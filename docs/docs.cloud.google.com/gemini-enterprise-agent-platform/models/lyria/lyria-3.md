---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/lyria/lyria-3
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/lyria/lyria-3
title: Lyria 3
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Lyria is a music generation model from Google. This page documents the capabilities and features of Lyria 3.

## 3 Pro Preview

[Try in Agent Studio](https://console.cloud.google.com/vertex-ai/studio/media/music)

Model ID

`lyria-3-pro-preview`

Modalities

description

Text  
Input only

photo

Image  
Input only

mic

Audio  
Output only

videocam

Video  
Not supported

Capabilities

  - [Text to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Image to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Vocal generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Instrumental mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Lyrics generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [User-provided lyrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Negative prompting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts)  
    Not supported
  - [Song generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Full song  
    Supported
  - [Detailed structure controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure)  
    Duration, BPM, Intensity  
    Supported
  - [Audio watermarking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Input, output (recitation), output (vocal likeness)  
    Supported
  - [Prompt rewriter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

Quotas

  - Regional online prediction requests per minute per base model: 10

Technical specifications

**Audio** mic

  - Maximum audio clip length: 184 seconds
  - Maximum number of clips per prompt: 1
  - Supported sample rates: 44.1 kHz
  - Supported bitrate: 192 kbps
  - Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese
  - Supported MIME types:
    `audio/mp3`

Supported regions

Model availability

Global

  - global

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Versions

`lyria-3-pro-preview`

  - Launch stage: Preview
  - Release date: 2026-03-25

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## 3 Clip Preview

[Try in Agent Studio](https://console.cloud.google.com/vertex-ai/studio/media/music)

Model ID

`lyria-3-clip-preview`

Modalities

description

Text  
Input only

photo

Image  
Input only

mic

Audio  
Output only

videocam

Video  
Not supported

Capabilities

  - [Text to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Image to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Vocal generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Instrumental mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Lyrics generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [User-provided lyrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Negative prompting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts)  
    Not supported
  - [Song generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    30 second clips  
    Supported
  - [Detailed structure controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure)  
    BPM, Intensity  
    Supported
  - [Audio watermarking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Input, output (recitation), output (vocal likeness)  
    Supported
  - [Prompt rewriter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported

Quotas

  - Regional online prediction requests per minute per base model: 10

Technical specifications

**Audio** mic

  - Maximum audio clip length: 30 seconds
  - Maximum number of clips per prompt: 1
  - Supported sample rates: 44.1 kHz
  - Supported bitrate: 192 kbps
  - Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese
  - Supported MIME types:
    `audio/mp3`

Supported regions

Model availability

Global

  - global

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Versions

`lyria-3-clip-preview`

  - Launch stage: Preview
  - Release date: 2026-03-25

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

For Lyria pricing information, see the [Lyria](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria) section of the [Cost of building and deploying AI models in Vertex AI](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria-models) page.
