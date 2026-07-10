---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro
title: Gemini 3.1 Pro
description: Learn about Gemini 3.1 Pro, our most advanced reasoning model, capable of solving complex problems across text, audio, images, video, PDFs, and code with a 1M token window.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

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

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-3.1-pro-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-3.1-pro-preview) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3.1-pro-preview)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3.1-pro-preview`

Modalities

description

Text  
Input and output

photo

Image  
Input only

mic

Audio  
Input only

videocam

Video  
Input only

Token limits

Context window

1,048,576

Maximum output tokens

65,536

Capabilities

  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Supported
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)  
    Supported
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)  
    Not supported
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)  
    Supported
  - [Context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)  
    Implicit context caching, explicit context caching  
    Supported
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)  
    Supported
  - [RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)  
    Not supported
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)  
    Supported
  - [Tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models)  
    Not supported
  - [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context)  
    Supported

Tools

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)  
    Google Search, Parallel Web Search, Exa Web Search  
    Supported
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)  
    Supported
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Supported
  - [Computer Use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) preview Preview feature  
    Not supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Standard PayGo, Flex PayGo, Priority PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Technical specifications

**Image** photo

  - Maximum images per prompt: 3000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Default resolution tokens: 1120
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Text** description

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

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

Knowledge cutoff date

January 2025

Versions

`gemini-3.1-pro-preview`

  - Launch stage: Public preview
  - Release date: February 19, 2026

`gemini-3.1-pro-preview-customtools*`

  - Launch stage: Public preview
  - Release date: February 23, 2026

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

<sup>\*</sup> Provisioned Throughput (PT) is not supported for this endpoint.
