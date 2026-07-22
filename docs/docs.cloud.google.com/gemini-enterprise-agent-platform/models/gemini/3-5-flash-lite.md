---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite
title: Gemini 3.5 Flash-Lite
description: Learn about Gemini 3.5 Flash-Lite, our low-latency, minimal cost model optimized for coding tasks, precise document understanding, and lightweight agentic workflows.
data_source: docs.cloud.google.com
---

Gemini 3.5 Flash-Lite is the latest in our cost-effective Flash-Lite line of models. It's optimized for simple coding tasks, precise document understanding, and lightweight agentic workflows that require fast inference at minimal cost. 3.5 Flash-Lite is a suitable replacement model for Gemini 2.5 Flash and less complex Gemini 3 Flash workloads.

When using 3.5 Flash-Lite, you can use different thinking levels to optimize for quality, speed, and token output:

  - **Use `thinking_level.MINIMAL` for latency-sensitive or simpler classification and extraction tasks** : 3.5 Flash-Lite defaults to minimal thinking, which optimizes for speed and cost efficiency. This is ideal for high-throughput classification, routing, or JSON extraction tasks.
  - **Use `thinking_level.MEDIUM` or `thinking_level.HIGH` for subagents** : If you're using 3.5 Flash-Lite as an autonomous subagent that writes code, runs terminal commands, or calls external APIs, set the thinking level to medium or high. Using the minimal thinking level can cause premature tool termination on multi-step tasks.

3.5 Flash-Lite includes the following potentially breaking changes when compared to previous Gemini models:

  - **Custom values for parameters like temperature, top-K, and top-P aren't supported.** If you set a custom value for these parameters, that value will be ignored.
  - **Custom values for frequency and presence penalty parameters aren't supported.** Setting a custom value for these parameters will throw an error.
  - API requests where the last input turn has a role of `Model` aren't supported. The following kinds of requests will return an error:
      - When using the Interactions API: Requests where the last object in the `input` array has `"type": "model_output"` .
      - When using the GenerateContent API: Requests where the last object in the `contents` array has `"role": "model"` .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/chat?model=gemini-3.5-flash-lite) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/chat?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3.5-flash-lite) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3.5-flash-lite`

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
  - Multi-region: `us` , `eu`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - Multi-region: `us` , `eu`

**[Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models)**

  - Global: `global`
  - Multi-region: `us` , `eu`

**[Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)**

  - Global: `global`
  - Multi-region: `us` , `eu`

Versions

`gemini-3.5-flash-lite`

  - Launch stage: GA
  - Release date: July 21, 2026
  - Retirement date: July 21, 2027 or later

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
