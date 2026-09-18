---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/omni-1-1-flash
title: Gemini Omni 1.1 Flash Preview
description: Learn about Gemini Omni 1.1 Flash Preview, which is optimized for video generation and multimodal tasks.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini Omni 1.1 Flash (Preview) is a multimodal model designed for video, image, and text tasks. It is optimized for video generation, offering video output alongside text responses in a single model.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-omni-1.1-flash-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-omni-1.1-flash-preview) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-omni-1.1-flash-preview) [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Note: "Deploy example app" requires a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-omni-1.1-flash-preview`

Modalities

description

Text  
Input and output

photo

Image  
Input only

mic\_off

Audio  
Not supported

videocam

Video  
Input and output

Token limits

Maximum input tokens

131,072

Maximum output tokens

57,920

Capabilities

  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Supported
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)  
    Not supported
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)  
    Not supported
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)  
    Not supported
  - [Context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)  
    Not supported
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)  
    Supported
  - [RAG Engine](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview)  
    Not supported
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)  
    Not supported
  - [Tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tune-models)  
    Not supported
  - [URL context](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context)  
    Not supported
  - [Image generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation)  
    Not supported
  - [Edit images](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/gemini-edit-images)  
    Not supported
  - [Interleaved images and text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/image-generation#interleaved-images)  
    Not supported
  - [Generate videos from text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-text)  
    Supported
  - [Generate videos from an image](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-an-image)  
    Supported
  - [Generate videos from references](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-references)  
    Supported
  - [Videos from first and last frames](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/generate-videos-from-first-and-last-frames)  
    Supported
  - [Sound generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/video-gen-prompt-guide#audio)  
    Speech, music, sound effects  
    Supported
  - [Video editing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/edit-videos)  
    Supported
  - [Extend videos](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/video/extend-videos)  
    Supported
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)  
    Supported
  - [Agentic video understanding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing) preview Preview feature  
    Not supported

Tools

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)  
    Not supported
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)  
    Not supported
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Not supported
  - [Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) preview Preview feature  
    Not supported

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

**Image** photo

  - Maximum images per prompt: 10
  - Maximum file size per file for inline data or direct uploads through the console: 20 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Text** description

  - Maximum file size per file for the API or Cloud Storage imports: 50 MB
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Supported MIME types:
    `text/plain`

**Video** videocam

  - Maximum video length (with audio): 10 seconds
  - Maximum video length (without audio): 10 seconds
  - Maximum number of videos per prompt: 3
  - Supported aspect ratios: 16:9, 9:16
  - Supported resolutions: 360p, 720p, 1080p, 4k
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

**Parameter defaults** tune

  - Temperature: 0.0-2.0 (default 1.0)
  - topP: 0.0-1.0 (default 0.95)
  - candidateCount: 1

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

**[Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)**

  - Global: `global`

Versions

`gemini-omni-1.1-flash-preview`

  - Launch stage: Preview
  - Release date: August 27, 2026
