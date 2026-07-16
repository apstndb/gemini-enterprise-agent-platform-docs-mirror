---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api
title: Gemini 2.5 Flash with Gemini Live API
description: Learn about Gemini 2.5 Flash with Gemini Live API, featuring cutting-edge audio functionality.
data_source: docs.cloud.google.com
---

Gemini 2.5 Flash with Gemini Live API native audio features our cutting-edge native audio functionality for [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) . In addition to the standard Gemini Live API features, this model includes:

  - **Enhanced audio quality:** Experience dramatically improved audio quality that feels like speaking with a person.
  - **Enhanced voice quality and adaptability:** Gemini Live API native audio provides richer, more natural voice interactions with [30 HD voices](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#voice_options) in [24 languages](https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd#language_availability) .
  - **Introducing [Proactive Audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-gemini-capabilities#use-proactive-audio) :** (Preview) When Proactive Audio is enabled, the model only responds when it's relevant. The model generates text transcripts and audio responses proactively only for queries directed to the device, and does not respond to non-device directed queries.
  - **Introducing Affective Dialog:** Models using Gemini Live API native audio can understand and respond appropriately to users' emotional expressions for more nuanced conversations.
  - **Improved barge-in:** Interrupt Gemini more naturally and reliably, even in loud and noisy environments.
  - **Robust function calling:** We've improved the triggering rate, allowing Gemini to successfully execute the functions you define to support your use cases.
  - **Accurate transcription:** The accuracy of audio-to-text transcription has been significantly enhanced. For even better results, you can provide language hints to guide the model toward the correct language. For more information, see [Enable audio transcription for the session](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#enable-audio-transcription) .
  - **Seamless multilingual support:** Speak to Gemini in multiple languages, and it will effortlessly switch between them without any pre-configuration. Language is no longer a barrier.

For more information on Gemini Live API, see:

  - Our [standalone Gemini Live API documentation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) .
  - Our [Gemini Live API supported audio formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api#supported-audio-formats) .
  - Our [Gemini Live API concurrent session limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#max-concurrent-sessions) .

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal-live?model=gemini-live-2.5-flash-native-audio) [View pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`gemini-live-2.5-flash-native-audio`

Modalities

description

Text  
Input and output

photo

Image  
Input only

mic

Audio  
Input and output

videocam

Video  
Input only

Token limits

Context window

128K

Maximum output tokens

64K

Maximum concurrent sessions

[1000](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#maximum_concurrent_sessions)

Capabilities

  - [Thinking](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking)  
    Not supported
  - [System instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction)  
    Supported
  - [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)  
    Supported
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

Tools

  - [Grounding](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview)  
    Google Search  
    Supported
  - [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution)  
    Not supported
  - [Function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling)  
    Supported
  - [Computer Use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use) preview Preview feature  
    Not supported

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

  - Maximum images per prompt: 3,000
  - Maximum file size per file for inline data or direct uploads through the console: 7 MB
  - Maximum file size per file from Google Cloud Storage: 30 MB
  - Supported MIME types:
    `image/png` , `image/jpeg` , `image/webp` , `image/heic` , `image/heif`

**Video** videocam

  - Standard resolution: 768 x 768
  - Supported MIME types:
    `video/x-flv` , `video/quicktime` , `video/mpeg` , `video/mpegs` , `video/mpg` , `video/mp4` , `video/webm` , `video/wmv` , `video/3gpp`

**Audio** mic

  - Maximum conversation length: Default 10 minutes that can [be extended.](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session#session-extension)
  - Required audio input format: Raw 16-bit PCM audio at 16kHz, little-endian
  - Required audio output format: Raw 16-bit PCM audio at 24kHz, little-endian
  - Supported MIME types:
    `audio/x-aac` , `audio/flac` , `audio/mp3` , `audio/m4a` , `audio/mpeg` , `audio/mpga` , `audio/mp4` , `audio/ogg` , `audio/pcm` , `audio/wav` , `audio/webm`

**Parameter defaults** tune

  - Start of speech sensitivity: Low
  - End of speech sensitivity: High
  - Prefix padding: 0
  - Max context size: 128K

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - United States: `us-central1` , `us-east1` , `us-east4` , `us-east5` , `us-south1` , `us-west1` , `us-west4`
  - Europe: `europe-central2` , `europe-north1` , `europe-southwest1` , `europe-west1` , `europe-west4` , `europe-west8`

Versions

`gemini-live-2.5-flash-native-audio`

  - Launch stage: GA
  - Release date: December 12, 2025
  - Retirement date: December 13, 2026

Security controls

**Online prediction**

  - Data residency
  - CMEK
  - VPC-SC
  - AXT

See [Security controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls) for more information.
