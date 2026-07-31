---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/vto/virtual-try-on-001
title: Virtual Try-On
description: Learn about the Virtual Try-On model (virtual-try-on-001), which lets you generate virtual try-on images.
data_source: docs.cloud.google.com
---

The Virtual Try-On model ( `virtual-try-on-001` ) lets you generate virtual try-on images from an image of a person and product photos that you provide.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/generate;tab=image) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`virtual-try-on-001`

Modalities

description

Text  
Not supported

photo

Image  
Input and output

mic

Audio  
Not supported

videocam

Video  
Not supported

Capabilities

  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Not supported
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)  
    Not supported
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)  
    Not supported
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
  - [Virtual try-on](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/virtual-try-on)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

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

**Image** photo

  - Maximum images per prompt: 2
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum number of output images per prompt: 4
  - Supported aspect ratios: Same as input image
  - Supported resolutions: Same as input image
  - Supported MIME types:
    `image/png` , `image/jpeg`

**Parameter defaults** tune

  - candidateCount: 1-4

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1` , `us-east1` , `us-east4` , `us-east5` , `us-south1` , `us-west1` , `us-west4`
  - Canada: `northamerica-northeast1`
  - Europe: `europe-west1` , `europe-west4` , `europe-west8` , `europe-west9` , `europe-southwest1` , `europe-north1`
  - Asia Pacific: `asia-northeast1` , `asia-southeast1`
  - Middle East: `me-central1`

**[ML processing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency)**

Not supported.

**[Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)**

  - United States: `us-central1` , `us-east1` , `us-east4` , `us-east5` , `us-south1` , `us-west1` , `us-west4`
  - Canada: `northamerica-northeast1`
  - Europe: `europe-west1` , `europe-west4` , `europe-west8` , `europe-west9` , `europe-southwest1` , `europe-north1`
  - Asia Pacific: `asia-northeast1` , `asia-southeast1`
  - Middle East: `me-central1`

**[Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/supported-models)**

  - United States: `us-central1` , `us-east1` , `us-east4` , `us-east5` , `us-south1` , `us-west1` , `us-west4`
  - Canada: `northamerica-northeast1`
  - Europe: `europe-west1` , `europe-west4` , `europe-west8` , `europe-west9` , `europe-southwest1` , `europe-north1`
  - Asia Pacific: `asia-northeast1` , `asia-southeast1`
  - Middle East: `me-central1`

Versions

`virtual-try-on-001`

  - Launch stage: GA
  - Release date: January 20, 2026
  - Retirement date: January 20, 2027
