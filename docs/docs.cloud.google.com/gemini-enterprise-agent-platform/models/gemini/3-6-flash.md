---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash
title: Gemini 3.6 Flash
description: Learn about Gemini 3.6 Flash, our model optimized for multi-step orchestration, full-stack code refactoring, and general reasoning.
data_source: docs.cloud.google.com
---

Gemini 3.6 Flash is optimized for multi-step orchestration, full-stack code refactoring, and general reasoning. It improves on many key areas critical to the Flash line of models.

Improvements from previous Flash models include:

  - **Improved token efficiency** over Gemini 3.5 Flash. 3.6 Flash uses less tokens and completes multi-step workflows in fewer turns.
  - **Improved code generation** with lower compile-failure and revision rates across building, prototyping, and IDE agent environments.
  - **Reduces action bias** by resolving read-only diagnostic tasks without making unsolicited edits.
  - **Improved multimodal reasoning** with respect to chart interpretation, visual blueprint conversion, and multi-element web layout generation.

Flash includes the following potentially breaking changes when compared to previous Gemini models:

  - **Custom values for parameters like temperature, top-K, and top-P aren't supported.** If you set a custom value for these parameters, that value will be ignored.
  - **Custom values for frequency and presence penalty parameters aren't supported.** Setting a custom value for these parameters will throw an error.
  - API requests where the last input turn has a role of `Model` aren't supported. The following kinds of requests will return an error:
      - When using the Interactions API: Requests where the last object in the `input` array has `"type": "model_output"` .
      - When using the GenerateContent API: Requests where the last object in the `contents` array has `"role": "model"` .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-3.6-flash) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/chat?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3.6-flash) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3.6-flash`

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
    Supported
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)  
    Supported
  - [Tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models)  
    Not supported
  - [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context)  
    Supported

Tools

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)  
    Google Search, Google Maps  
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

  - Maximum images per prompt: 3,000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Maximum number of output images per prompt: 10
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Text** description

  - Maximum number of files per prompt: 3,000
  - Maximum number of pages per file: 3,000
  - Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Supported MIME types:
    `application/pdf` , `text/plain`

**Video** videocam

  - Maximum video length (with audio): Approximately 45 minutes
  - Maximum video length (without audio): Approximately 1 hour
  - Maximum number of videos per prompt: 10
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

**Audio** mic

  - Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens
  - Maximum number of audio files per prompt: 1
  - Supported MIME types:
    `audio/x-aac` , `audio/flac` , `audio/mp3` , `audio/m4a` , `audio/mpeg` , `audio/mpga` , `audio/mp4` , `audio/ogg` , `audio/pcm` , `audio/wav` , `audio/webm`

**Parameter defaults** tune

  - Temperature: 1.0
  - topP: 0.95
  - topK: 64
  - Frequency penalty: 0
  - Presence penalty: 0

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

**[Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models)**

  - Global: `global`

**[Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)**

  - Global: `global`

Versions

`gemini-3.6-flash`

  - Launch stage: GA
  - Release date: July 21, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**Batch inference**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**Context caching**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.
