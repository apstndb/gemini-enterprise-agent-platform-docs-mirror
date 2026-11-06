---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-2-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-2-flash
title: Gemini Omni 1.2 Flash
description: Learn about Gemini Omni 1.2 Flash, a multimodal model optimized for video generation, editing, extension, and upscaling alongside text responses.
data_source: docs.cloud.google.com
---

Gemini Omni 1.2 Flash is a multimodal model designed for video, image, and text tasks. Omni 1.2 Flash is optimized for video generation, editing, extension, and standalone video upscaling, generating or editing video output with synchronized audio up to 15 seconds at 360p, 720p, 1080p, or 4K resolution alongside text responses in a single model.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-omni-1.2-flash) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-omni-1.2-flash) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-omni-1.2-flash) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

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
<th><code>gemini-omni-1.2-flash</code></th>
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
mic_off
Audio<br />
Not supported
videocam
Video<br />
Input and output</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Maximum input tokens</th>
<td>131,072</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>260,640</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation">Image generation</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images">Edit images</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation#interleaved-images">Interleaved images and text</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text">Generate videos from text</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image">Generate videos from an image</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references">Generate videos from references</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames">Videos from first and last frames</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio">Sound generation</a><br />
Speech, music, sound effects<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/edit-videos">Video editing</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos">Extend videos</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/upscale-videos">Upscale videos</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a><br />
Not supported</li>
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
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
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<th><strong>Image</strong> photo</th>
<td><ul>
<li>Maximum images per prompt: 10</li>
<li>Maximum file size per file for inline data or direct uploads through the console: 20 MB</li>
<li>Maximum file size per file from Google Cloud Storage: 30 MB</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/heic</code> , <code>image/heif</code></li>
</ul></td>
</tr>
<tr class="even">
<th><strong>Text</strong> description</th>
<th><ul>
<li>Maximum file size per file for the API or Cloud Storage imports: 50 MB</li>
<li>Maximum file size per file for direct uploads through the console: 7 MB</li>
<li>Supported MIME types:
<code>text/plain</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Maximum video length (with audio): 15 seconds</li>
<li>Maximum video length (without audio): 15 seconds</li>
<li>Maximum input video length (video understanding): 10 minutes</li>
<li>Maximum input video length (editing): 15 seconds</li>
<li>Maximum input video length (extension): Any duration (uses up to the last 10 seconds)</li>
<li>Maximum input video length (upscaling): 15 seconds</li>
<li>Output video duration (generation and editing): 3 to 15 seconds (3 to 10 seconds for first and last frames)</li>
<li>Output video duration (extension): 3 to 10 seconds (concatenated onto up to the last 30 seconds of the input video)</li>
<li>Maximum number of videos per prompt: 3</li>
<li>Supported aspect ratios: 16:9, 9:16</li>
<li>Supported resolutions: 360p, 720p, 1080p, 4k</li>
<li>Supported MIME types:
<code>video/x-flv</code> , <code>video/quicktime</code> , <code>video/mpeg</code> , <code>video/mpegs</code> , <code>video/mpg</code> , <code>video/mp4</code> , <code>video/webm</code> , <code>video/wmv</code> , <code>video/3gpp</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Parameter defaults</strong> tune</th>
<th><ul>
<li>Temperature: 0.0-2.0 (default 1.0)</li>
<li>topP: 0.0-1.0 (default 0.95)</li>
<li>candidateCount: 1</li>
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
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models">Provisioned Throughput</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-omni-1.2-flash</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: November 5, 2026</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-2-flash#retirement-date">†</a></sup> : November 5, 2027 or later</li>
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

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .
