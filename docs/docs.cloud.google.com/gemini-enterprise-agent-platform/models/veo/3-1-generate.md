---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate
title: Veo&nbsp;3.1
description: Learn about Veo&nbsp;3, Google's newest line of video generation models.
data_source: docs.cloud.google.com
---

Veo 3.1 is our latest line of video generation models. This page documents the capabilities and features of Veo 3.1.

## 3.1 Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>veo-3.1-generate-001</code></td>
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
mic_off
Audio<br />
Not supported
videocam
Video<br />
Output only</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text">Video generation</a><br />
Text to video, image to video, from first and last frame<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos">Extend videos</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references">Use reference images</a><br />
Asset images<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio">Sound generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
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
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td><strong>Video</strong> videocam</td>
<td><ul>
<li>Video lengths: 4, 6, or 8 seconds; reference image to video only supports 8 seconds.</li>
<li>Maximum number of output videos per prompt: 4</li>
<li>Image-to-video maximum input image size: 20 MB</li>
<li>Supported aspect ratios: 9:16, 16:9</li>
<li>Supported input resolutions: 720p, 1080p</li>
<li>Supported output resolutions: 720p, 1080p, 4K</li>
<li>Supported framerates: 24 FPS</li>
<li>Supported MIME types:
<code>video/mp4</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Prompt languages</th>
<td><ul>
<li>English</li>
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
<th>Quotas</th>
<td><ul>
<li><strong>Regional online prediction requests per base model per minute per base model</strong> : 50 tokens per minute</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>veo-3.1-generate-001</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: November 17, 2025</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#retirement-date">†</a></sup> : November 17, 2026 or later</li>
</ul></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Security controls</th>
<td><strong>Online prediction</strong></td>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .

## 3.1 Fast Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>veo-3.1-fast-generate-001</code></td>
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
mic_off
Audio<br />
Not supported
videocam
Video<br />
Output only</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text">Video generation</a><br />
Text to video, image to video, from first and last frame<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos">Extend videos</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references">Use reference images</a><br />
Asset images<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio">Sound generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
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
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td><strong>Video</strong> videocam</td>
<td><ul>
<li>Video lengths: 4, 6, or 8 seconds.</li>
<li>Maximum number of output videos per prompt: 4</li>
<li>Image-to-video maximum input image size: 20 MB</li>
<li>Supported aspect ratios: 9:16, 16:9</li>
<li>Supported input resolutions: 720p, 1080p</li>
<li>Supported output resolutions: 720p, 1080p</li>
<li>Supported framerates: 24 FPS</li>
<li>Supported MIME types:
<code>video/mp4</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Prompt languages</th>
<td><ul>
<li>English</li>
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
<th>Quotas</th>
<td><ul>
<li><strong>Regional online prediction requests per base model per minute per base model</strong> : 50 tokens per minute</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>veo-3.1-fast-generate-001</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: November 17, 2025</li>
<li>Retirement date <sup><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate#retirement-date">†</a></sup> : November 17, 2026 or later</li>
</ul></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Security controls</th>
<td><strong>Online prediction</strong></td>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<td></td>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

## 3.1 Lite Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>veo-3.1-lite-generate-001</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Input only
hide_image
Image<br />
Not supported
mic_off
Audio<br />
Not supported
videocam
Video<br />
Output only</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text">Video generation</a><br />
Text to video, image to video, from first and last frame<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos">Extend videos</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references">Use reference images</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio">Sound generation</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials">Content Credentials (C2PA)</a><br />
Supported</li>
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
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Technical specifications</th>
<td><strong>Video</strong> videocam</td>
<td><ul>
<li>Video lengths: 4, 6, or 8 seconds.</li>
<li>Maximum number of output videos per prompt: 4</li>
<li>Image-to-video maximum input image size: 20 MB</li>
<li>Supported aspect ratios: 9:16, 16:9</li>
<li>Supported input resolutions: 720p, 1080p</li>
<li>Supported output resolutions: 720p, 1080p</li>
<li>Supported framerates: 24 FPS</li>
<li>Supported MIME types:
<code>video/mp4</code></li>
</ul></td>
</tr>
<tr class="even">
<th>Prompt languages</th>
<td><ul>
<li>English preview Preview feature</li>
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
<th>Quotas</th>
<td><ul>
<li><strong>Regional online prediction requests per base model per minute per base model</strong> : 50 tokens per minute</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>veo-3.1-lite-generate-001</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: April 2, 2026</li>
</ul></li>
</ul></td>
<td></td>
</tr>
</tbody>
</table>

<sup>†</sup> Listed retirement dates refer to retirement of support in Gemini Enterprise Agent Platform. Models may remain accessible through the Gemini API after these dates have passed. The Gemini API is not a Google Cloud offering and is subject to its own terms of service. For details, see the [Gemini API documentation](https://ai.google.dev/) .

For Veo pricing information, see the [Veo](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#veo) section of the [Cost of building and deploying AI models in Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.
