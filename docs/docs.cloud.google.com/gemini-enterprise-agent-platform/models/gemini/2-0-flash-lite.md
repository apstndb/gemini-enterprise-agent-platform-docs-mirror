---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-0-flash-lite
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-0-flash-lite
title: Gemini 2.0 Flash-Lite
description: Learn about Gemini 2.0 Flash-Lite, the fastest Gemini 2.0 model, optimized for cost efficiency and low latency.
data_source: docs.cloud.google.com
---

> **Caution:** As of March 6, 2026, `gemini-2.0-flash-001` and `gemini-2.0-flash-lite-001` are only available for existing customers. This includes both model serving and Provisioned Throughput. New projects should use `gemini-2.5-flash` , `gemini-2.5-flash-lite` , or more recent releases.

Gemini 2.0 Flash-Lite is our fastest Gemini 2.0 model, optimized for cost efficiency and low latency.

[Try in Agent Platform](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-2.0-flash-lite-001) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/gemini-2.0-flash-lite-001) [(Preview) Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-2.0-flash-lite-001)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-2.0-flash-lite`

Supported inputs & outputs

  - Inputs:
    Text , Code , Images , Audio , Video
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1,048,576
  - Maximum output tokens: 8,192 (default)

Capabilities

Supported

  - [Supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)
  - [Tuning checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning-checkpoints)
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)
  - [Explicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)

Not supported

  - [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)
  - [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-continuous-tuning)
  - [Preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-preference-tuning)
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)
  - [Implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)
  - [Vertex AI RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Consumption options

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Standard PayGo with Usage Tiers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)

Not supported

  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)
  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Input size limit

500 MB

Technical specifications

**Images** photo

  - Maximum images per prompt: 3,000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Maximum tokens per minute (TPM):
      - High/Medium/Default media resolution:
          - US/Asia: 6.7 M
          - EU: 2.6 M
      - Low media resolution:
          - US/Asia: 2.6 M
          - EU: 2.6 M
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Documents** description

  - Maximum number of files per prompt: 3,000
  - Maximum number of pages per file: 1,000
  - Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Maximum tokens per minute (TPM) per project1:
      - US/Asia: 3.4 M
      - EU: 3.4 M
  - Supported MIME types:

**Video** videocam

  - Maximum video length (with audio): Approximately 45 minutes
  - Maximum video length (without audio): Approximately 1 hour
  - Maximum number of videos per prompt: 10
  - Maximum tokens per minute (TPM):
      - High/Medium/Default media resolution:
          - US/Asia: 6.3 M
          - EU: 3.2 M
      - Low media resolution:
          - US/Asia: 3.2 M
          - EU: 3.2 M
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

**Audio** mic

  - Maximum audio length per prompt: Approximately 8.4 hours, or up to 1 million tokens
  - Maximum number of audio files per prompt: 1
  - Speech understanding for: Audio summarization, transcription, and translation
  - Maximum tokens per minute (TPM):
      - US/Asia: 3.5 M
      - EU: 3.5 M
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

United States

  - us-central1
  - us-east1
  - us-east4
  - us-east5
  - us-south1
  - us-west1
  - us-west4

Europe

  - europe-central2
  - europe-north1
  - europe-southwest1
  - europe-west1
  - europe-west4
  - europe-west8
  - europe-west9

ML processing

United States

  - Multi-region

Europe

  - Multi-region

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

June 2024

Versions

`gemini-2.0-flash-lite-001`

  - Launch stage: GA
  - Release date: February 25, 2025
  - Discontinuation date: June 1, 2026

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

**Tuning**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**RAG Engine**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**Context caching**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**Grounding with Google Search and Grounding with Google Maps**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

Supported languages

See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1) .

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
