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

Model ID

`lyria-3-pro-preview`

Supported inputs & outputs

  - Inputs:
    Text , Image
  - Outputs:
    Audio

Capabilities

Supported

  - [Text to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Image to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Full song generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Vocal generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Instrumental mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Lyrics generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [User-provided lyrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Duration controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure) preview Preview feature
  - [BPM controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure) preview Preview feature
  - [Intensity controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure) preview Preview feature
  - [Audio watermarking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Input filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Output filtering - recitation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Output filtering - vocal likeness](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Prompt rewriter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature

Not supported

  - [Negative prompting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts)

Technical specifications

**Audio** mic

  - Maximum audio clip length: 184 seconds
  - Maximum number of clips per prompt: 1
  - Supported sample rates: 44.1 kHz
  - Supported bitrate: 192 kbps
  - Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese
  - Supported MIME types:
    `audio/mp3`

Versions

`lyria-3-pro-preview`

  - Launch stage: Preview
  - Release date: 2026-03-25

Quotas

  - Regional online prediction requests per minute per base model: 10

## 3 Clip Preview

Model ID

`lyria-3-clip-preview`

Supported inputs & outputs

  - Inputs:
    Text , Image
  - Outputs:
    Audio

Capabilities

Supported

  - [Text to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Image to music](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [30s clip generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Vocal generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Instrumental mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Lyrics generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [User-provided lyrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [BPM controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure) preview Preview feature
  - [Intensity controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure) preview Preview feature
  - [Audio watermarking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Input filtering](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Output filtering - recitation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Output filtering - vocal likeness](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature
  - [Prompt rewriter](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/generate-music) preview Preview feature

Not supported

  - [Negative prompting](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#negative-prompts)
  - [Duration controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/music/music-gen-prompt-guide#detailed-structure)

Technical specifications

**Audio** mic

  - Maximum audio clip length: 30 seconds
  - Maximum number of clips per prompt: 1
  - Supported sample rates: 44.1 kHz
  - Supported bitrate: 192 kbps
  - Supported languages: English, German, Spanish, French, Hindi, Japanese, Korean, and Portuguese
  - Supported MIME types:
    `audio/mp3`

Versions

`lyria-3-clip-preview`

  - Launch stage: Preview
  - Release date: 2026-03-25

Quotas

  - Regional online prediction requests per minute per base model: 10

For Lyria pricing information, see the [Lyria](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria) section of the [Cost of building and deploying AI models in Vertex AI](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#lyria-models) page.
