---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live
title: Gemini 3.8 Live
description: Learn about Gemini 3.8 Live, offering improved voice quality, reliability, and real-time agent orchestration.
data_source: docs.cloud.google.com
---

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal-live?model=gemini-3.8-live) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`gemini-3.8-live`

Modalities

description

Text  
Input and output

photo

Image  
Input only

mic

Audio  
Input and output

videocam

Video  
Input and output

Token limits

Maximum input tokens

128K

Maximum output tokens

64K

Capabilities

  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Not supported
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)  
    Supported
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)  
    Supported
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)  
    Not supported
  - [Context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)  
    Not supported
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)  
    Not supported
  - [RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)  
    Not supported
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)  
    Not supported
  - [Tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models)  
    Not supported
  - [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context)  
    Not supported
  - [Agentic video understanding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing) preview Preview feature  
    Not supported

Tools

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)  
    Google Search  
    Supported
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)  
    Not supported
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Supported
  - [Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) preview Preview feature  
    Not supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Standard PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Technical specifications

**Text** description

  - Supported MIME types:
    `text/plain`

**Image** photo

  - Supported resolutions: Minimum: 704x1280 or 1280x704
  - Supported aspect ratios: Portrait, Landscape
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Audio** mic

  - Maximum number of audio files per prompt: 1-stream
  - Required audio input format: Raw 16-bit PCM audio at 16kHz, little-endian
  - Required audio output format: Raw 16-bit PCM audio at 24kHz, little-endian
  - Supported MIME types:
    `audio/x-aac` , `audio/flac` , `audio/mp3` , `audio/m4a` , `audio/mpeg` , `audio/mpga` , `audio/mp4` , `audio/ogg` , `audio/pcm` , `audio/wav` , `audio/webm` , `audio/mpa`

**Video** videocam

  - Supported resolutions: Minimum: 704x1280 or 1280x704
  - Supported aspect ratios: Portrait, Landscape
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Multi-region: `us` , `eu`
  - United States: `us-central1`

**[Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models)**

  - Multi-region: `us` , `eu`
  - United States: `us-central1`

**[Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)**

  - Multi-region: `us` , `eu`
  - United States: `us-central1`

Knowledge cutoff date

January 2025

Versions

`gemini-3.8-live`

  - Launch stage: GA
  - Release date: September 24, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.
