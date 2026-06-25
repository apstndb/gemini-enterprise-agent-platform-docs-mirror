---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-flash
title: Gemini 3 Flash
description: Learn about Gemini 3 Flash, Google's latest Gemini Flash model.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini 3 Flash combines Gemini 3 Pro's reasoning capabilities with the Flash line's levels on latency, efficiency, and cost. It not only enables everyday tasks with improved reasoning, but is designed to tackle the most complex agentic workflows.

Gemini 3 Flash uses several new features to improve performance, control, and multimodal fidelity:

  - **Thinking level** : Use the `thinking_level` parameter to control the amount of internal reasoning the model performs ( *minimal* , *low* , *medium* , or *high* ) to balance response quality, reasoning complexity, latency, and cost. The `thinking_level` parameter replaces `thinking_budget` for Gemini 3 models.
    
    > **Note:** If you used a thinking budget of `0` with Gemini 2.5 Flash, set your thinking level to `MINIMAL` for similar latency and cost; however, you still need to handle thought signatures when using the *minimal* thinking level.
    
    For details on the different thinking levels, see [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking#gemini-3-and-later-models) .

  - **Thought signatures** : Stricter validation of [thought signatures](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thought-signatures) improves reliability in multi-turn function calling.

  - **Media resolution** : Use the `media_resolution` parameter ( *low* , *medium* , *high* , or *ultra high* ) to control vision processing for multimodal inputs, impacting token usage and latency. See [Get started with Gemini 3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3#media_resolution) for default resolution settings.
    
      - The *ultra high* media resolution level is only available for the `IMAGE` modality.
      - PDF token counts will be listed under the `IMAGE` modality instead of the `DOCUMENT` modality in `usage_metadata` .

  - **Multimodal function responses** : Function responses can now include [multimodal objects like images and PDFs in addition to text](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling#mm-fr) .

  - **Streaming Function calling** : [Stream partial function call arguments](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling#streaming-fc) to improve user experience during tool use.

For more information on using these features, see [Get started with Gemini 3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/get-started-with-gemini-3) .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal?model=gemini-3-flash-preview) [View in Model Garden](https://console.cloud.google.com/agent-platform/publishers/google/model-garden/gemini-3-flash-preview) [Deploy example app](https://console.cloud.google.com/agent-platform/studio/multimodal?suggestedPrompt=How%20does%20AI%20work&deploy=true&model=gemini-3-flash-preview)

Note: To use the "Deploy example app" feature, you need a Google Cloud project with billing and Agent Platform API enabled.

Model ID

`gemini-3-flash-preview`

Supported inputs & outputs

  - Inputs:
    Text , Image , Audio , Video
  - Outputs:
    Text

Token limits

  - Maximum input tokens: 1,048,576
  - Maximum output tokens: 65,536

Capabilities

Supported

  - [Grounding with Google Search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-google-search)
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)
  - [Structured output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output)
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)
  - [Count Tokens](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count)
  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)
  - [Implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Explicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview)
  - [Chat completions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview)
  - [Computer Use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) preview Preview feature

Not supported

  - [Supervised fine-tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-supervised-tuning)
  - [Continuous tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-continuous-tuning)
  - [Preference tuning](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-preference-tuning)
  - [Tuning checkpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning-checkpoints)
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)
  - [Content Credentials (C2PA)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/content-credentials)

Consumption options

Supported

  - [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput)
  - [Standard PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo)
  - [Flex PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/flex-paygo)
  - [Priority PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/priority-paygo)
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)

Not supported

See [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) for more information.

Technical specifications

**Images** photo

  - Maximum images per prompt: 3000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Default resolution tokens: 1120
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Documents** description

  - Maximum number of files per prompt: 3000
  - Maximum number of pages per file: 3000
  - Maximum file size per file for the API or Cloud Storage imports: 50 MB(application/pdf) or 7 MB(text/plain)
  - Maximum file size per file for direct uploads through the console: 7 MB
  - Default resolution tokens: 560
  - OCR for scanned PDFs: Not used by default
  - Supported MIME types:
    `application/pdf` , `text/plain`

**Video** videocam

  - Maximum video length (with audio): Approximately 45 minutes
  - Maximum video length (without audio): Approximately 1 hour
  - Maximum number of videos per prompt: 10
  - Default resolution tokens per frame: 70
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

See [Deployments and endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) for more information.

Knowledge cutoff date

January 2025

Versions

`gemini-3-flash-preview`

  - Launch stage: Public preview
  - Release date: December 17, 2025

Supported languages

See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/google-models#expandable-1) .

Pricing

See [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
