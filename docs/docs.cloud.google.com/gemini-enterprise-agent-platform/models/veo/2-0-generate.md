---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/2-0-generate
title: Veo&nbsp;2
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Caution:** The following table describes image generation endpoints that are deprecated and their replacements. We recommend updating your model endpoints before June 30, 2026, to avoid service disruption.
> 
> | Discontinued endpoints      | Recommended endpoint migration |
> | --------------------------- | ------------------------------ |
> | `veo-3.0-generate-001`      | `veo-3.1-generate-001`         |
> | `veo-3.0-fast-generate-001` | `veo-3.1-fast-generate-001`    |
> | `veo-2.0-generate-001`      | `veo-3.1-generate-001`         |
> 

Veo 2 is our stable line of video generation models. This page documents the capabilities and features of Veo 2.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video)

Model ID

`veo-2.0-generate-001`

Modalities

description

Text  
Input only

photo

Image  
Not supported

mic

Audio  
Not supported

videocam

Video  
Output only

Capabilities

  - [Video generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)  
    Text to video, image to video  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Not supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Style images, asset images  
    Supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Not supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Not supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Not supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Supported

Technical specifications

**Video** videocam

  - Video lengths: 5 to 8 seconds
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p
  - Supported input resolutions: 720p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`
  - Europe: `europe-west3`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 10 tokens per minute

Versions

`veo-2.0-generate-001`

  - Launch stage: GA
  - Release date: May 27, 2025
  - Deprecation date: June 30, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

For Veo pricing information, see the [Veo](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#veo) section of the [Cost of building and deploying AI models in Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.
