---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro
title: Gemini 3.1 Pro
description: Learn about Gemini 3.1 Pro, our most advanced reasoning model, capable of solving complex problems across text, audio, images, video, PDFs, and code with a 1M token window.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . You can process personal data for this product or feature as outlined in the [Cloud Data Processing Addendum](https://docs.cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud. Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Gemini 3.1 Pro is our most advanced reasoning Gemini model, capable of solving complex problems. Gemini 3.1 Pro can comprehend vast datasets and challenging problems from different information sources, including text, audio, images, video, PDFs, and even entire code repositories with its 1M token context window.

For more information on using the latest Gemini models, see [Get started with Gemini 3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3) .

## Quality improvements

Gemini 3.1 Pro includes several quality improvements:

  - **Improved SWE and agentic capabilities** : Improved software engineering behavior and usability, with agentic improvements in domains like finance and spreadsheet applications.
  - **Improved token efficiency and thinking** : More efficient thinking across various use cases.
  - **Expanded thinking levels** : Introduces `MEDIUM` as a `thinking_level` parameter for more options to optimize trade-offs between cost, performance, and speed.

## Custom tools endpoint

For those building with a mix of bash and custom tools, Gemini 3.1 Pro supports an additional endpoint: `gemini-3.1-pro-preview-customtools` . This endpoint is better at prioritizing custom tools (such as `view_file` or `search_code` ). As `gemini-3.1-pro-preview-customtools` is optimized for agentic workflows that use custom tools and bash, you may see quality fluctuations in some use cases which don't benefit from such tools.

Pricing for `gemini-3.1-pro-preview-customtools` is identical to Gemini 3.1 Pro. Provisioned Throughput (PT) is not supported on `gemini-3.1-pro-preview-customtools` .

[Try in Agent Platform](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-3.1-pro-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/gemini-3.1-pro-preview) [(Preview) Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3.1-pro-preview)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3.1-pro-preview`

Supported inputs & outputs

  - Inputs:
    Text , Code , Images , Audio , Video , PDF
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1,048,576
  - Maximum output tokens: 65,536

Capabilities

Supported

  - [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)
  - [Implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Explicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Vertex AI RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)

Not supported

  - [Supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)
  - [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-continuous-tuning)
  - [Preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-preference-tuning)
  - [Tuning checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning-checkpoints)
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Consumption options

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)
  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)

Not supported

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Technical specifications

**Images** photo

  - Maximum images per prompt: 3000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Default resolution tokens: 1120
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Documents** description

  - Maximum number of files per prompt: 3000
  - Maximum number of pages per file: 3000
  - Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Default resolution tokens: 560
  - OCR for scanned PDFs: Not used by default
  - Supported MIME types:
    `application/pdf` , `text/plain`

**Video** videocam

  - Maximum video length (with audio): Approximately 45 minutes
  - Maximum video length (without audio): Approximately 1 hour
  - Maximum number of videos per prompt: 10
  - Default resolution tokens per frame: 70
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

**Audio** mic

  - Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens
  - Maximum number of audio files per prompt: 1
  - Speech understanding for: Audio summarization, transcription, and translation
  - Supported MIME types:
    `audio/x-aac` , `audio/flac` , `audio/mp3` , `audio/m4a` , `audio/mpeg` , `audio/mpga` , `audio/mp4` , `audio/ogg` , `audio/pcm` , `audio/wav` , `audio/webm`

**Parameter defaults** tune

  - Temperature: 0.0-2.0 (default 1.0)
  - topP: 0.0-1.0 (default 0.95)
  - topK: 64 (fixed)
  - candidateCount: 1–8 (default 1)

Supported regions

Model availability

Global

  - global

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

January 2025

Versions

`gemini-3.1-pro-preview`

  - Launch stage: Public preview
  - Release date: February 19, 2026

`gemini-3.1-pro-preview-customtools*`

  - Launch stage: Public preview
  - Release date: February 23, 2026

Supported languages

See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1) .

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

<sup>\*</sup> Provisioned Throughput (PT) is not supported for this endpoint.
