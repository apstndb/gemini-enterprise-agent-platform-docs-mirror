---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/embedding-2
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/embedding-2
title: Gemini Embedding 2
description: Learn about Gemini Embedding 2, Google's omnimodal embedding model designed to generate 3072-dimensional vectors.
data_source: docs.cloud.google.com
---

Gemini Embedding 2 is Google's embedding generation model that's ideal for complex retrieval and analytics tasks.

Gemini Embedding 2 accepts multimodal inputs to generate 3072-dimensional vectors. It accepts images, text, documents, audio, and video inputs and semantically maps the generated vectors into a unified semantic space. This lets you perform tasks, such as searching for an image based on a text description.

Gemini Embedding 2 introduces several features to optimize embedding quality and flexibility:

- **Custom task instructions:** By specifying task instructions (for example, `task:code retrieval` or `task:search result` ) optimize the embeddings for the intended relationships and retrieve more accurate results for the specific goal.

- **Adjustable result size:** The model generates a 3072-dimensional float vector, by default. However, you can retrieve a smaller dimensional output by specifying the `output_dimensionality` parameter.

- **Document OCR:** Read OCR from document inputs.

- **Audio track extraction:** Extract audio tracks from video inputs and interleave them with video frames.

For more information on how to use Gemini Embedding 2, see [Get multimodal embeddings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/get-multimodal-embeddings) .

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
<th><code>gemini-embedding-2</code></th>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<th>description
Text<br />
Input only
photo
Image<br />
Input only
mic
Audio<br />
Input only
videocam
Video<br />
Input only
graph_3
Embeddings<br />
Output only</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Maximum input tokens</th>
<td>8,192</td>
</tr>
<tr class="even">
<th>Maximum output tokens</th>
<th>N/A</th>
<td></td>
</tr>
<tr class="odd">
<th>Output dimensions</th>
<th>Up to 3,072 (with MRL support)</th>
<td></td>
</tr>
<tr class="even">
<th>Maximum sequence length</th>
<th>8,192 tokens</th>
<td></td>
</tr>
<tr class="odd">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/embeddings/batch-prediction-genai-embeddings">Batch inference</a><br />
Supported</li>
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
<li>Maximum input tokens: 8,192</li>
<li>Maximum number of files per prompt: 1</li>
<li>Maximum number of pages per file (for PDF): 6</li>
<li>Maximum file size per file: N/A</li>
<li>OCR for scanned PDFs: Not used by default</li>
<li>Supported MIME types:
<code>text/plain</code> , <code>application/pdf</code></li>
</ul></td>
</tr>
<tr class="odd">
<th><strong>Image</strong> photo</th>
<th><ul>
<li>Maximum images per prompt: 6</li>
<li>Maximum file size per file for inline data or direct uploads through the console: No limit</li>
<li>Maximum file size per file from Google Cloud Storage: No limit</li>
<li>Maximum number of output images per prompt: N/A</li>
<li>Supported MIME types:
<code>image/png</code> , <code>image/jpeg</code> , <code>image/webp</code> , <code>image/bmp</code> , <code>image/heic</code> , <code>image/heif</code> , <code>image/avif</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th><strong>Video</strong> videocam</th>
<th><ul>
<li>Maximum video length (with audio): 80 seconds</li>
<li>Maximum video length (without audio): 120 seconds</li>
<li>Maximum number of videos per prompt: 1</li>
<li>Supported MIME types:
<code>video/mpeg</code> , <code>video/mp4</code></li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th><strong>Audio</strong> mic</th>
<th><ul>
<li>Maximum audio length per prompt: 180 seconds</li>
<li>Maximum number of audio files per prompt: 1</li>
<li>Supported MIME types:
<code>audio/mp3</code> , <code>audio/wav</code></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
<li>United States multi-region: <code>us</code></li>
<li>Europe multi-region: <code>eu</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Knowledge cutoff date</th>
<th>November 2025</th>
<td></td>
</tr>
<tr class="even">
<th>Versions</th>
<th><ul>
<li><code>gemini-embedding-2</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: April 22, 2026</li>
</ul></li>
<li><code>gemini-embedding-2-preview</code>
<ul>
<li>Launch stage: Public preview</li>
<li>Release date: March 10, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
</tbody>
</table>
