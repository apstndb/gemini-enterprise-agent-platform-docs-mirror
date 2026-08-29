---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-0-generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-0-generate
title: Veo&nbsp;3
description: Learn about Veo&nbsp;3, Google's newest line of video generation models.
data_source: docs.cloud.google.com
---

> **Caution:** The following table describes image generation endpoints that are deprecated and their replacements. We recommend updating your model endpoints before June 30, 2026, to avoid service disruption.
> 
> | Discontinued endpoints      | Recommended endpoint migration |
> | --------------------------- | ------------------------------ |
> | `veo-3.0-generate-001`      | `veo-3.1-generate-001`         |
> | `veo-3.0-fast-generate-001` | `veo-3.1-fast-generate-001`    |
> 

Veo 3 is our latest line of video generation models. This page documents the capabilities and features of Veo 3.

## 3.0 Generate 001

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.0-generate-001`

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
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos)  
    Not supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)  
    Not supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Not supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Supported

Technical specifications

**Video** videocam

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 10 tokens per minute

Versions

`veo-3.0-generate-001`

  - Launch stage: GA
  - Release date: July 29, 2025
  - Retirement date: June 30, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

## 3.0 Fast Generate 001

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.0-fast-generate-001`

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
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos)  
    Not supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)  
    Not supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

Consumption options

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)  
    Supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Not supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Supported

Technical specifications

**Video** videocam

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 10 tokens per minute

Versions

`veo-3.0-fast-generate-001`

  - Launch stage: GA
  - Release date: July 29, 2025
  - Retirement date: June 30, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

For Veo pricing information, see the [Veo](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#veo) section of the [Cost of building and deploying AI models in Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.
