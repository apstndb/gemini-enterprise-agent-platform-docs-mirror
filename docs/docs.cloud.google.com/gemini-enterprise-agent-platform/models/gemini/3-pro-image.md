---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-pro-image
title: Gemini 3 Pro Image
description: Learn about Gemini 3 Pro Image, which is a reasoning model ideal for complex and multi-turn image generation and editing.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) , as well as the [Additional Terms for Generative AI Preview Products](https://docs.cloud.google.com/trustedtester/aitos) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, disclose Generated Output to third-parties, and process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

Gemini 3 Pro Image, or Gemini 3 Pro (with Nano Banana), is designed to tackle the most challenging image generation by incorporating state-of-the-art reasoning capabilities. It's the best model for complex and multi-turn image generation and editing, having improved accuracy and enhanced image quality.

For more information about image generation using Gemini 3 Pro Image, see [Generate and edit images with Gemini](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation) .

[Try in Agent Platform](https://console.cloud.google.com/vertex-ai/generative/multimodal/create/text?model=gemini-3-pro-image-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-3-pro-image-preview) [(Preview) Deploy example app](https://console.cloud.google.com/vertex-ai/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3-pro-image-preview)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3-pro-image-preview`

Supported inputs & outputs

  - Inputs:
    Text , Images
  - Outputs:
    Text and image

Token limits

  - Maximum input tokens: 65,536
  - Maximum output tokens: 32,768

Capabilities

Supported

  - [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)
  - [Image generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation)
  - [Interleaved images and text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation#interleaved-images)
  - [Edit images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)
  - [Multi-turn image editing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images#multi-turn-editing)

Not supported

  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)
  - [Supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)
  - [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-continuous-tuning)
  - [Preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-preference-tuning)
  - [Tuning checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning-checkpoints)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)
  - [Implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Explicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Vertex AI RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)

Consumption options

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)
  - [Batch prediction](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-prediction-gemini)

Not supported

  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Input size limit

500 MB

Technical specifications

**Images** photo

  - Maximum images per prompt: 14
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Maximum number of output images per prompt: Limited to 32,768 output tokens
  - Supported aspect ratios: 1:1, 3:2, 2:3, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, and 21:9
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Documents** description

  - Maximum number of files per prompt: As supported by the 65,536 token context window
  - Maximum number of pages per file: As supported by the 65,536 token context window
  - Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Supported MIME types:
    `application/pdf` , `text/plain`

**Parameter defaults** tune

  - Temperature: 0.0-2.0
  - topP: 0.0-1.0 (default 0.95)
  - topK: 64 (fixed)
  - candidateCount: 1

Supported regions

Model availability

Global

  - global

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

January 2025

Versions

`gemini-3-pro-image-preview`

  - Launch stage: Public preview
  - Release date: November 20, 2025

Supported languages

See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1) .

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
