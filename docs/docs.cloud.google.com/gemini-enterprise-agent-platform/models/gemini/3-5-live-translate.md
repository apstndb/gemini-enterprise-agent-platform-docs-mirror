---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-live-translate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-live-translate
title: Gemini 3.5 Live Translate
description: Learn about Gemini 3.5 Live Translate, our model optimized for low-latency, real-time speech-to-speech translation between 70+ languages.
data_source: docs.cloud.google.com
---

Gemini 3.5 Live Translate supports low-latency, real-time speech-to-speech translation between 70+ languages using the `gemini-3.5-live-translate-preview` model, available through Agent Platform. By configuring the Live API with translation settings, you can stream audio in one language and receive translated audio output in another language, enabling seamless real-time voice-to-voice translation.

To get started, view the [introductory notebook for Gemini 3.5 Live Translate](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_5_live_translate.ipynb)

## Live streaming translation

The `BidiGenerateContent` (Live) API maintains a persistent, bidirectional WebSocket connection. You stream raw audio chunks to the session and receive translated audio chunks and optional transcripts in real time.

    import asyncio
    from google import genai
    from google.genai import types
    
    # Initialize the client for Vertex AI / Agent Platform
    client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)
    
    model = "gemini-3.5-live-translate-preview"
    config = types.LiveConnectConfig(
        response_modalities=["AUDIO"],
        input_audio_transcription=types.AudioTranscriptionConfig(),
        output_audio_transcription=types.AudioTranscriptionConfig(),
        translation_config=types.TranslationConfig(
            target_language_code="pl",
            echo_target_language=True,
        ),
    )
    
    async def streaming_translation(audio_stream_generator):
        async with client.aio.live.connect(model=model, config=config) as session:
            # In a complete implementation, stream audio chunks concurrently:
            # async for chunk in audio_stream_generator:
            #     await session.send_realtime_input(
            #         audio=types.Blob(data=chunk, mime_type="audio/pcm;rate=16000")
            #     )
    
            async for response in session.receive():
                if response.server_content:
                    server_content = response.server_content
    
                    if server_content.input_transcription:
                        print(f"Input transcript: {server_content.input_transcription.text}")
    
                    if server_content.output_transcription:
                        print(f"Output transcript: {server_content.output_transcription.text}")
    
                    if server_content.model_turn:
                        for part in server_content.model_turn.parts:
                            if part.inline_data:
                                translated_audio_chunk = part.inline_data.data
                                # Process or stream translated audio (24kHz PCM)
                                print(f"Received translated audio: {len(translated_audio_chunk)} bytes")

## Audio specifications

Stream audio as raw, little-endian, 16-bit linear PCM:

  - Input format: 16-bit linear PCM at 16kHz (mono, little-endian).

  - Output format: 16-bit linear PCM at 24kHz (mono, little-endian).

  - Streaming chunk size: Chunks of 100ms duration are recommended for optimal balance between throughput and latency.

<!-- end list -->

    # Streaming an audio chunk to an active session
    await session.send_realtime_input(
        audio=types.Blob(
            data=pcm_bytes,
            mime_type="audio/pcm;rate=16000",
        )
    )

## Configuration

Live Translation is configured by attaching a `TranslationConfig` to your `LiveConnectConfig` .

### Configuration parameters

  - **`target_language_code`** *(string)* : The [BCP-47 language code](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-live-translate#supported-languages) for the desired output language (e.g., `"pl"` , `"es"` , `"ja"` ). Defaults to `"en"` .
  - **`echo_target_language`** *(boolean)* : Controls behavior when spoken input is already in the target language:
      - `True` : The model reproduces and echoes the input speech in the output stream.
      - `False` : The model remains silent when input matches the target language. Defaults to `False` .
  - **`input_audio_transcription`** *(AudioTranscriptionConfig)* : Optional. Enables synchronized text transcription for the incoming source audio.
  - **`output_audio_transcription`** *(AudioTranscriptionConfig)* : Optional. Enables synchronized text transcription for the outgoing translated audio.

## Language support

The following languages and BCP-47 language codes are supported for Gemini 3.5 Live Translate:

| Language              | BCP-47 Code | Language              | BCP-47 Code |
| :-------------------- | :---------- | :-------------------- | :---------- |
| Afrikaans             | `af`        | Kazakh                | `kk`        |
| Akan                  | `ak`        | Khmer                 | `km`        |
| Albanian              | `sq`        | Kinyarwanda           | `rw`        |
| Amharic               | `am`        | Korean                | `ko`        |
| Arabic                | `ar`        | Lao                   | `lo`        |
| Armenian              | `hy`        | Latvian               | `lv`        |
| Azerbaijani           | `az`        | Lithuanian            | `lt`        |
| Basque                | `eu`        | Macedonian            | `mk`        |
| Belarusian            | `be`        | Malay                 | `ms`        |
| Bengali               | `bn`        | Malayalam             | `ml`        |
| Bulgarian             | `bg`        | Marathi               | `mr`        |
| Burmese (Myanmar)     | `my`        | Mongolian             | `mn`        |
| Catalan               | `ca`        | Nepali                | `ne`        |
| Chinese (Simplified)  | `zh-Hans`   | Norwegian             | `no` , `nb` |
| Chinese (Traditional) | `zh-Hant`   | Persian               | `fa`        |
| Croatian              | `hr`        | Polish                | `pl`        |
| Czech                 | `cs`        | Portuguese (Brazil)   | `pt-BR`     |
| Danish                | `da`        | Portuguese (Portugal) | `pt-PT`     |
| Dutch                 | `nl`        | Punjabi               | `pa`        |
| English               | `en`        | Romanian              | `ro`        |
| Estonian              | `et`        | Russian               | `ru`        |
| Filipino              | `fil`       | Serbian               | `sr`        |
| Finnish               | `fi`        | Sindhi                | `sd`        |
| French                | `fr`        | Sinhala               | `si`        |
| Galician              | `gl`        | Slovak                | `sk`        |
| Georgian              | `ka`        | Slovenian             | `sl`        |
| German                | `de`        | Spanish               | `es`        |
| Greek                 | `el`        | Sundanese             | `su`        |
| Gujarati              | `gu`        | Swahili               | `sw`        |
| Hausa                 | `ha`        | Swedish               | `sv`        |
| Hebrew                | `he`        | Tamil                 | `ta`        |
| Hindi                 | `hi`        | Telugu                | `te`        |
| Hungarian             | `hu`        | Thai                  | `th`        |
| Icelandic             | `is`        | Turkish               | `tr`        |
| Indonesian            | `id`        | Ukrainian             | `uk`        |
| Italian               | `it`        | Urdu                  | `ur`        |
| Japanese              | `ja`        | Uzbek                 | `uz`        |
| Javanese              | `jv`        | Vietnamese            | `vi`        |
| Kannada               | `kn`        | Zulu                  | `zu`        |

## Best practices

  - Maintain consistent sampling: Ensure audio input strictly adheres to 16kHz mono PCM to prevent pitch shifts and audio artifacts.

  - Handle acoustic environments: While the model filters moderate ambient noise, strong background chatter or overlapping speakers can introduce translation ambiguity.

  - Evaluate echo mode per use case: Set echo\_target\_language=False for one-way interpreter setups to suppress unnecessary rebroadcasting when speakers already use the target language.

[Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`['gemini-3.5-live-translate-preview']`

Modalities

description

Text  
Output only

hide\_image

Image  
Not supported

mic

Audio  
Input and output

videocam\_off

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
    Not supported
  - [Batch inference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference)  
    Not supported
  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Not supported
  - [Fixed quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas)  
    Not supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

Versions

`gemini-3.5-live-translate-preview`

  - Launch stage: Preview
  - Release date: August 2026
