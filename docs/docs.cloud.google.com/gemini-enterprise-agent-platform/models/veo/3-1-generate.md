---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-1-generate
title: Veo&nbsp;3.1
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Veo 3.1 is our latest line of video generation models. This page documents the capabilities and features of Veo 3.1.

## 3.1 Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.1-generate-001`

Modalities

description

Text  
Input only

photo

Image  
Input only

mic

Audio  
Not supported

videocam

Video  
Output only

Capabilities

  - [Video generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)  
    Text to video, image to video, from first and last frame  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Asset images  
    Supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Not supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Not supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Not supported
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

  - Video lengths: 4, 6, or 8 seconds; reference image to video only supports 8 seconds.
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported input resolutions: 720p, 1080p
  - Supported output resolutions: 720p, 1080p, 4K
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 50 tokens per minute

Versions

`veo-3.1-generate-001`

  - Launch stage: GA
  - Release date: November 17, 2025

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

## 3.1 Fast Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.1-fast-generate-001`

Modalities

description

Text  
Input only

photo

Image  
Input only

mic

Audio  
Not supported

videocam

Video  
Output only

Capabilities

  - [Video generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)  
    Text to video, image to video, from first and last frame  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Asset images  
    Supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Not supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Not supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Not supported
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

  - Video lengths: 4, 6, or 8 seconds.
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported input resolutions: 720p, 1080p
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

  - **Regional online prediction requests per base model per minute per base model** : 50 tokens per minute

Versions

`veo-3.1-fast-generate-001`

  - Launch stage: GA
  - Release date: November 17, 2025

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

## 3.1 Lite Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.1-lite-generate-001`

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
    Text to video, image to video, from first and last frame  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Not supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Not supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Not supported
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

  - Video lengths: 4, 6, or 8 seconds.
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported input resolutions: 720p, 1080p
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English preview Preview feature

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 50 tokens per minute

Versions

`veo-3.1-lite-generate-001`

  - Launch stage: Preview
  - Release date: April 2, 2026

> **Caution:** The following table describes the video generation preview endpoints that will be deprecated and removed on April 2, 2026. Migrate any workflows using preview models to the recommended GA endpoints.
> 
> | Discontinued endpoints          | Recommended endpoint migration |
> | ------------------------------- | ------------------------------ |
> | `veo-2.0-generate-exp`          | `veo-2.0-generate-001`         |
> | `veo-2.0-generate-preview`      | `veo-2.0-generate-001`         |
> | `veo-3.0-generate-preview`      | `veo-3.0-generate-001`         |
> | `veo-3.0-fast-generate-preview` | `veo-3.0-fast-generate-001`    |
> | `veo-3.1-generate-preview`      | `veo-3.1-generate-001`         |
> | `veo-3.1-fast-generate-preview` | `veo-3.1-fast-generate-001`    |
> 

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

## 3.1 Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.1-generate-preview`

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
    Text to video, image to video, from first and last frame  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Asset images  
    Supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Not supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Not supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Not supported
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

  - Video lengths: 4, 6, or 8 seconds; reference image-to-video only supports 8 seconds.
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p, 4k
  - Supported input resolutions: 720p, 1080p, 4k
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English preview Preview feature

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 10 tokens per minute

Versions

`veo-3.1-generate-preview`

  - Launch stage: Preview
  - Release date: October 15, 2025
  - Deprecation date: April 2, 2026

> **Caution:** The following table describes the video generation preview endpoints that will be deprecated and removed on April 2, 2026. Migrate any workflows using preview models to the recommended GA endpoints.
> 
> | Discontinued endpoints          | Recommended endpoint migration |
> | ------------------------------- | ------------------------------ |
> | `veo-2.0-generate-exp`          | `veo-2.0-generate-001`         |
> | `veo-2.0-generate-preview`      | `veo-2.0-generate-001`         |
> | `veo-3.0-generate-preview`      | `veo-3.0-generate-001`         |
> | `veo-3.0-fast-generate-preview` | `veo-3.0-fast-generate-001`    |
> | `veo-3.1-generate-preview`      | `veo-3.1-generate-001`         |
> | `veo-3.1-fast-generate-preview` | `veo-3.1-fast-generate-001`    |
> 

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

## 3.1 Fast Generate

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/media/video) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`veo-3.1-fast-generate-preview`

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
    Text to video, image to video, from first and last frame  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)  
    Supported
  - [Use reference images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation)  
    Asset images  
    Supported
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Not supported
  - [Insert objects into videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/insert-objects-into-videos) preview Preview feature  
    Not supported
  - [Remove objects from videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/remove-objects-from-videos) preview Preview feature  
    Not supported
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

  - Video lengths: 4, 6, or 8 seconds.
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p, 4k
  - Supported input resolutions: 720p, 1080p, 4k
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Prompt languages

  - English preview Preview feature

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1`

Quotas

  - **Regional online prediction requests per base model per minute per base model** : 50 tokens per minute

Versions

`veo-3.1-fast-generate-preview`

  - Launch stage: Preview
  - Release date: October 15, 2025
  - Deprecation date: April 2, 2026

For Veo pricing information, see the [Veo](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#veo) section of the [Cost of building and deploying AI models in Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.
