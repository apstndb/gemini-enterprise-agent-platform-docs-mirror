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

[Try in Agent Studio](https://console.cloud.google.com/vertex-ai/generative/multimodal/create/text?model=gemini-embedding-2) [Deploy example app](https://console.cloud.google.com/vertex-ai/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-embedding-2)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-embedding-2`

Supported inputs & outputs

  - Inputs:
    Text , Images , Audio , Video , PDF
  - Outputs:
    Embeddings

Token limits

  - Maximum input tokens: 8,192
  - Maximum output tokens: N/A

Maximum sequence length

8,192 tokens

Output dimensions

Up to 3,072 (with MRL support)

Consumption options

Supported

  - [Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)
  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)
  - [Batch prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Technical specifications

**Images** photo

  - Maximum images per prompt: 6
  - Maximum file size per file for inline data or direct uploads through the console: No limit
  - Maximum file size per file from Google Cloud Storage: No limit
  - Maximum number of output images per prompt: N/A
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/bmp` , `image/heic` , `image/heif` , `image/avif`

**Documents** description

  - Maximum number of files per prompt: 1
  - Maximum number of pages per file: 6
  - Maximum file size per file: N/A
  - Supported MIME types:
    `application/pdf`

**Video** videocam

  - Maximum video length (with audio): 80 seconds
  - Maximum video length (without audio): 120 seconds
  - Maximum number of videos per prompt: 1
  - Supported MIME types:
    `video/mpeg` , `video/mp4`

**Audio** mic

  - Maximum audio length per prompt: 180 seconds
  - Maximum number of audio files per prompt: 1
  - Supported MIME types:
    `audio/mp3` , `audio/wav`

**Parameter defaults** tune

Supported regions

Model availability

Global

  - global

United States multi-region (See [connection guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations#specify-an-endpoint) )

  - us

Europe multi-region (See [connection guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations#specify-an-endpoint) )

  - eu

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

November 2025

Versions

`gemini-embedding-2`

  - Launch stage: GA
  - Release date: April 22, 2026

`gemini-embedding-2-preview`

  - Launch stage: Public preview
  - Release date: March 10, 2026

Security controls

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

Supported languages

See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1) .

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
