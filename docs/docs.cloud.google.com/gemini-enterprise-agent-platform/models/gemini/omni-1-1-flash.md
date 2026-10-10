---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash
title: Gemini Omni 1.1 Flash Preview
description: Learn about Gemini Omni 1.1 Flash Preview, which is optimized for video generation and multimodal tasks.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini Omni 1.1 Flash (Preview) is a multimodal model designed for video, image, and text tasks. It is optimized for video generation, offering video output alongside text responses in a single model.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-omni-1.1-flash-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-omni-1.1-flash-preview) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-omni-1.1-flash-preview) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

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
<th><code>gemini-omni-1.1-flash-preview</code></th>
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
<th>57,920</th>
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
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
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
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
Not supported</li>
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
<li>Maximum video length (with audio): 10 seconds</li>
<li>Maximum video length (without audio): 10 seconds</li>
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
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo">Standard PayGo</a></strong></p></th>
<th><ul>
<li>Global: <code>global</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<th><ul>
<li><code>gemini-omni-1.1-flash-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: August 27, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
</tbody>
</table>
