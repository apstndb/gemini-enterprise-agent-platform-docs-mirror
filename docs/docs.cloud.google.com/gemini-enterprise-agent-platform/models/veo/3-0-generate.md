---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-0-generate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/veo/3-0-generate
title: Veo&nbsp;3
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

Veo 3 is our latest line of video generation models. This page documents the capabilities and features of Veo 3.

## 3.0 Generate 001

Model ID

veo-3.0-generate-001

Supported inputs & outputs

  - Inputs:
    Text
  - Outputs:
    Video

Capabilities

Supported

  - [Text to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)
  - [Image to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Not supported

  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)
  - [Generate videos from the first and last frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)
  - [Reference style images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-style-images)
  - [Reference asset images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-subject-images)

Usage types

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

Technical specifications

**Videos**

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Versions

`veo-3.0-generate-001`

  - Launch stage: GA
  - Release date: July 29, 2025
  - Discontinuation date: June 30, 2026

Prompt languages

  - English

Quotas

  - Regional online prediction requests per base model per minute per base model: 10

## 3.0 Fast Generate 001

Model ID

veo-3.0-fast-generate-001

Supported inputs & outputs

  - Inputs:
    Text
  - Outputs:
    Video

Capabilities

Supported

  - [Text to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)
  - [Image to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off)
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Not supported

  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)
  - [Generate videos from the first and last frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)
  - [Reference style images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-style-images)
  - [Reference asset images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-subject-images)

Usage types

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

Technical specifications

**Videos**

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 4
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Versions

`veo-3.0-fast-generate-001`

  - Launch stage: GA
  - Release date: July 29, 2025
  - Discontinuation date: June 30, 2026

Prompt languages

  - English

Quotas

  - Regional online prediction requests per base model per minute per base model: 10

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

> **Preview with production use**
> 
> The Image-to-Video feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) , as well as the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties. Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

## 3.0 Generate

Model ID

veo-3.0-generate-preview

Supported inputs & outputs

  - Inputs:
    Text
  - Outputs:
    Video

Capabilities

Supported

  - [Text to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text) preview Preview feature
  - [Image to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image) preview Preview feature
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off) preview Preview feature
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio) preview Preview feature
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Not supported

  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)
  - [Generate videos from the first and last frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)
  - [Reference style images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-style-images)
  - [Reference asset images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-subject-images)

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

Technical specifications

**Videos**

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 2
  - Image-to-video maximum input image size: 20 MB
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Versions

`veo-3.0-generate-preview`

  - Launch stage: Preview
  - Release date: May 20, 2025
  - Discontinuation date: April 2, 2026

Prompt languages

  - English preview Preview feature

Quotas

  - Regional online prediction requests per base model per minute per base model: 10

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

> **Preview with production use**
> 
> The Image-to-Video feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) , as well as the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties. Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products#product-launch-stages) .

## 3.0 Fast Generate

Model ID

veo-3.0-fast-generate-preview

Supported inputs & outputs

  - Inputs:
    Text
  - Outputs:
    Video

Capabilities

Supported

  - [Text to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text) preview Preview feature
  - [Image to video](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image) preview Preview feature
  - [Prompt rewriting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/turn-the-prompt-rewriter-off) preview Preview feature
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio) preview Preview feature
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Not supported

  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-a-veo-video)
  - [Generate videos from the first and last frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)
  - [Reference style images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-style-images)
  - [Reference asset images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/use-reference-images-to-guide-video-generation#use-subject-images)

Usage types

Supported

  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)

Not supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Dynamic shared quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)

Technical specifications

**Videos**

  - Video lengths: 4, 6, or 8 seconds
  - Maximum number of output videos per prompt: 2
  - Supported aspect ratios: 9:16, 16:9
  - Supported output resolutions: 720p, 1080p
  - Supported framerates: 24 FPS
  - Supported MIME types:
    `video/mp4`

Versions

`veo-3.0-fast-generate-preview`

  - Launch stage: Preview
  - Release date: July 07, 2025
  - Discontinuation date: April 2, 2026

Prompt languages

  - English preview Preview feature

Quotas

  - Regional online prediction requests per base model per minute per base model: 10

For Veo pricing information, see the [Veo](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#veo) section of the [Cost of building and deploying AI models in Agent Platform](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) page.
