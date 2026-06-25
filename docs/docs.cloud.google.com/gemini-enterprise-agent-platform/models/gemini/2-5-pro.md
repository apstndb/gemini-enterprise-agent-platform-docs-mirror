---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-pro
title: Gemini 2.5 Pro
description: Learn about Gemini 2.5 Pro, our most advanced reasoning Gemini model.
data_source: docs.cloud.google.com
---

Gemini 2.5 Pro is our most advanced reasoning Gemini model, capable of solving complex problems. Gemini 2.5 Pro can comprehend vast datasets and challenging problems from different information sources, including text, audio, images, video, and even entire code repositories.

For even more detailed technical information on Gemini 2.5 Pro (such as performance benchmarks, information on our training datasets, efforts on sustainability, intended usage and limitations, and our approach to ethics and safety), see our [technical report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v2_5_report.pdf) on our Gemini 2.5 models.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-2.5-pro) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-2.5-pro) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-2.5-pro)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-2.5-pro`

Supported inputs & outputs

  - Inputs:
    Text , Image , Audio , Video
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1,048,576
  - Maximum output tokens: 65,535 (default)

Capabilities

Supported

  - [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)
  - [Supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)
  - [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-continuous-tuning)
  - [Tuning checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning-checkpoints)
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)
  - [Implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Explicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)

Not supported

  - [Preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-preference-tuning)
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)

Consumption options

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Standard PayGo with Usage Tiers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)

Not supported

  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Input size limit

500 MB

Technical specifications

**Images** photo

  - Maximum images per prompt: 3,000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Documents** description

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

United States

  - us-central1
  - us-east1
  - us-east4
  - us-east5
  - us-south1
  - us-west1
  - us-west4

Canada

  - northamerica-northeast1

Europe

  - europe-central2
  - europe-north1
  - europe-southwest1
  - europe-west1
  - europe-west4
  - europe-west8
  - europe-west9

Asia Pacific

  - asia-northeast1

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

January 2025

Versions

`gemini-2.5-pro`

  - Launch stage: GA
  - Release date: June 17, 2025
  - Discontinuation date: Not before October 16, 2026

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

**Context caching**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

**RAG Engine**

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
