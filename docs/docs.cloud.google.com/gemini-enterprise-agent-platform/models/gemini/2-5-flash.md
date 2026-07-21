---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash
title: Gemini 2.5 Flash
description: Learn about Gemini 2.5 Flash, Google's balanced model in terms of price and performance, featuring thinking capabilities.
data_source: docs.cloud.google.com
---

Gemini 2.5 Flash is our best model in terms of price and performance, and offers well-rounded capabilities. Gemini 2.5 Flash is our first Flash model that features [thinking capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking) , which lets you see the thinking process that the model goes through when generating its response.

For even more detailed technical information on Gemini 2.5 Flash (such as performance benchmarks, information on our training datasets, efforts on sustainability, intended usage and limitations, and our approach to ethics and safety), see our [technical report](https://storage.googleapis.com/deepmind-media/gemini/gemini_v2_5_report.pdf) on our Gemini 2.5 models.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-2.5-flash) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-2.5-flash) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`gemini-2.5-flash`

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

65,535 (default)

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
    Supervised fine-tuning, continuous tuning, preference tuning, tuning checkpoints  
    Supported
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
    Priority PayGo  
    Supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Input size limit

500 MB

Technical specifications

**Image** photo

  - Maximum images per prompt: 3,000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
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
  - United States: `us-central1` , `us-east1` , `us-east4` , `us-east5` , `us-south1` , `us-west1` , `us-west4`
  - Canada: `northamerica-northeast1`
  - South America: `southamerica-east1`
  - Europe: `europe-central2` , `europe-north1` , `europe-southwest1` , `europe-west1` , `europe-west2` , `europe-west3` , `europe-west4` , `europe-west8` , `europe-west9`
  - Asia Pacific: `asia-northeast1` , `asia-northeast3` , `asia-south1` , `asia-southeast1` , `australia-southeast1`
  - Global: `global`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

  - United States: `Multi-region`
  - Canada: `northamerica-northeast1`
  - South America: `southamerica-east1`
  - Europe: `Multi-region` , `europe-west2` , `europe-west3` , `europe-west9`
  - Asia Pacific: `asia-northeast1` , `asia-northeast3` , `asia-south1` , `asia-southeast1` , `australia-southeast1`

Versions

`gemini-2.5-flash`

  - Launch stage: GA
  - Release date: June 17, 2025
  - Retirement date: October 16, 2026

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
