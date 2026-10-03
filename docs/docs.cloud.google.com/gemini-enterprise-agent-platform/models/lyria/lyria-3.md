---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/lyria/lyria-3
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/lyria/lyria-3
title: Lyria 3
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Lyria is a music generation model from Google. This page documents the capabilities and features of Lyria 3.

## 3 Pro Preview

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/music) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>lyria-3-pro-preview</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input only
photo
Image<br />
Input only
mic
Audio<br />
Output only
videocam_off
Video<br />
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Text to music</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Image to music</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Vocal generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Instrumental mode</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Lyrics generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">User-provided lyrics</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts">Negative prompting</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Song generation</a><br />
Full song<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure">Detailed structure controls</a><br />
Duration, BPM, Intensity<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Audio watermarking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Filtering</a><br />
Input, output (recitation), output (vocal likeness)<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Prompt rewriter</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<td><strong>Audio</strong> mic</td>
<td><ul>
<li>Maximum audio clip length: 184 seconds</li>
<li>Maximum number of clips per prompt: 1</li>
<li>Supported sample rates: 44.1 kHz</li>
<li>Supported bitrate: 192 kbps</li>
<li>Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese</li>
<li>Supported MIME types:
<code>audio/mp3</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Quotas</th>
<td><ul>
<li><strong>Regional online prediction requests per minute per base model</strong> : 10 tokens per minute</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>lyria-3-pro-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: 2026-03-25</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

## 3 Clip Preview

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/music) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>lyria-3-clip-preview</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input only
photo
Image<br />
Input only
mic
Audio<br />
Output only
videocam_off
Video<br />
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Text to music</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Image to music</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Vocal generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Instrumental mode</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Lyrics generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">User-provided lyrics</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts">Negative prompting</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Song generation</a><br />
30 second clips<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure">Detailed structure controls</a><br />
BPM, Intensity<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Audio watermarking</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Filtering</a><br />
Input, output (recitation), output (vocal likeness)<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music">Prompt rewriter</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Technical specifications</th>
<td><strong>Audio</strong> mic</td>
<td><ul>
<li>Maximum audio clip length: 30 seconds</li>
<li>Maximum number of clips per prompt: 1</li>
<li>Supported sample rates: 44.1 kHz</li>
<li>Supported bitrate: 192 kbps</li>
<li>Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese</li>
<li>Supported MIME types:
<code>audio/mp3</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Quotas</th>
<td><ul>
<li><strong>Regional online prediction requests per minute per base model</strong> : 10 tokens per minute</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>lyria-3-clip-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: 2026-03-25</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

For Lyria pricing information, see the [Lyria](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria) section of the [Cost of building and deploying AI models in Vertex AI](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria-models) page.
