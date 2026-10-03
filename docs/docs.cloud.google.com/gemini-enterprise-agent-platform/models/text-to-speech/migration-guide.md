---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide
title: Migrate to Gemini 3.8 TTS
description: Learn how to move from earlier Gemini TTS models and the Cloud Text-to-Speech API to the Gemini 3.8 TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

This page describes how to move from earlier Gemini TTS models, such as `gemini-3.1-flash-tts-preview` , `gemini-2.5-flash-tts` , `gemini-2.5-pro-tts` , and `gemini-2.5-flash-lite-preview-tts` , to [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` ) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ). The earlier models are documented in [Gemini-TTS](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts) in the Google Cloud Text-to-Speech documentation.

## Choose a replacement model

- **Gemini 3.8 Flash-Lite TTS** is the recommended replacement for `gemini-3.1-flash-tts-preview` . Choose it for high-volume production, voice agents, read-aloud features, and everyday single-speaker speech.
- **Gemini 3.8 Flash TTS** is the flagship model. Choose it when voice fidelity, acting nuance, multi-speaker dialogue, or dialect coverage matter most, such as for audiobooks and studio narration.

Both models use the same request schema, so you can switch between them by changing the model ID. For a comparison, see [When to use which model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#when-to-use-which-model) .

## Summary of changes

| Area                                   | Earlier Gemini TTS models                                                                                        | Gemini 3.8 TTS models                                                                                                                                                                                                                                                    |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| API                                    | Cloud Text-to-Speech API or Gemini Enterprise API                                                                | Gemini Enterprise API only ( `generateContent` and `streamGenerateContent` )                                                                                                                                                                                             |
| Location                               | `global` and regional endpoints                                                                                  | `global` only                                                                                                                                                                                                                                                            |
| Style direction                        | Written into the text ( `"Say the following in a curious way: ..."` ) or the Cloud Text-to-Speech `prompt` field | `speech_metadata.style` on each part                                                                                                                                                                                                                                     |
| Multi-speaker dialogue                 | Speaker prefixes in one text block, or Cloud Text-to-Speech `multiSpeakerMarkup`                                 | One part per turn with `speech_metadata.speaker`                                                                                                                                                                                                                         |
| Inline vocal tags                      | Square brackets, such as `[sigh]`                                                                                | Angle brackets, such as `<sigh>`                                                                                                                                                                                                                                         |
| Voice selection                        | `prebuiltVoiceConfig.voiceName`                                                                                  | `voiceConfig.voice` , which also accepts designed voice IDs and voice replication keys. `prebuiltVoiceConfig.voiceName` still works for prebuilt voices.                                                                                                                 |
| Custom voices                          | Inline reference audio in `replicatedVoiceConfig`                                                                | [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) and [voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) through the Voices API |
| Default output (Gemini Enterprise API) | Raw 16-bit PCM, 24 kHz, mono                                                                                     | Unary requests: a complete WAV file (16-bit PCM, 24 kHz, mono). Streaming requests: raw 16-bit PCM, unchanged. You can request other encodings with `responseFormat` .                                                                                                   |
| `temperature` , `topP` , `topK`        | Ignored                                                                                                          | Rejected with an `INVALID_ARGUMENT` error                                                                                                                                                                                                                                |

## Update your requests

1.  **Move style directions into `speech_metadata.style`** : The Gemini 3.8 TTS models read `text` as a verbatim transcript, so directions written into the text might be spoken aloud. Put sustained acting, tone, prosody, and pacing directions in `speech_metadata.style` .
2.  **Use one part per dialogue turn** : For multi-speaker dialogue, pass each turn as a separate `part` , and set `speech_metadata.speaker` on every turn to one of the speakers in `multiSpeakerVoiceConfig` .
3.  **Replace square-bracket tags with angle-bracket tags** : Use angle brackets, such as `<sigh>` , `<laugh>` , or `<short pause>` , only for point-in-time vocal events. Write disfluencies, such as "uhm", directly in the transcript.
4.  **Design personas upfront** : Replace long "Audio Profile" or "Director's Notes" prompts with a voice created in [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) , and keep `style` short or empty.
5.  **Remove unsupported parameters** : Remove `temperature` , `topP` , `topK` , `candidateCount` , and `systemInstruction` from your requests.
6.  **Handle WAV output from unary requests** : Unary requests now return a complete WAV file instead of raw PCM. If your code adds a WAV header or concatenates clips, remove the header step, or set `generationConfig.responseFormat` to `AUDIO_L16` to keep raw PCM output.
7.  **Recreate replicated voices with the Voices API** : Inline reference audio in `replicatedVoiceConfig` isn't supported. Create a stored voice or a voice replication key with the Voices API, and pass it in `voiceConfig.voice` . For details, see [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .

For more guidance on writing prompts, see the [prompting guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide) .

### Example

The following example shows a `gemini-3.1-flash-tts-preview` request and the equivalent Gemini 3.8 TTS request.

### Before Gemini 3.8

```
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.1-flash-tts-preview",
    contents="Say the following in a curious way: OK, so... tell me about this [uhm] AI thing.",
    config=types.GenerateContentConfig(
        response_modalities=["AUDIO"],
        speech_config=types.SpeechConfig(
            language_code="en-US",
            voice_config=types.VoiceConfig(
                prebuilt_voice_config=types.PrebuiltVoiceConfig(voice_name="Kore")
            ),
        ),
    ),
)
```

### Gemini 3.8 or later

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.8-flash-lite-tts",
    contents=[{
        "role": "user",
        "parts": [{
            "text": "OK, so... uhm, tell me about this AI thing.",
            "speech_metadata": {"style": "curious"},
        }],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {
            "language_code": "en-US",
            "voice_config": {"voice": "Kore"},
        },
    },
)
```

Both responses return the audio in `response.candidates[0].content.parts[0].inline_data.data` . The earlier model returns raw 16-bit PCM audio (24 kHz, mono), and the Gemini 3.8 TTS model returns a complete WAV file.

## Migrate from the Cloud Text-to-Speech API

If you call Gemini TTS through the Cloud Text-to-Speech API ( `texttospeech.googleapis.com` ), send your requests to the `generateContent` method on `aiplatform.googleapis.com` instead. The following table maps the Cloud Text-to-Speech request fields to the Gemini Enterprise API request fields:

| Cloud Text-to-Speech API ( `text:synthesize` )                                         | Gemini Enterprise API ( `generateContent` )                                                                                                                                              |
|----------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `input.text`                                                                           | `contents[].parts[].text`                                                                                                                                                                |
| `input.prompt`                                                                         | `contents[].parts[].speechMetadata.style`                                                                                                                                                |
| `input.multiSpeakerMarkup.turns[]` ( `speaker` , `text` )                              | One part per turn, with `text` and `speechMetadata.speaker`                                                                                                                              |
| `voice.modelName`                                                                      | The model ID in the request URL                                                                                                                                                          |
| `voice.name`                                                                           | `generationConfig.speechConfig.voiceConfig.voice`                                                                                                                                        |
| `voice.languageCode`                                                                   | `generationConfig.speechConfig.languageCode`                                                                                                                                             |
| `voice.multiSpeakerVoiceConfig.speakerVoiceConfigs[]` ( `speakerAlias` , `speakerId` ) | `generationConfig.speechConfig.multiSpeakerVoiceConfig.speakerVoiceConfigs[]` ( `speaker` , `voiceConfig.voice` )                                                                        |
| `audioConfig.audioEncoding` : `LINEAR16`                                               | `generationConfig.responseFormat[].audio.mimeType` : `AUDIO_WAV` (default for unary requests)                                                                                            |
| `audioConfig.audioEncoding` : `PCM`                                                    | `AUDIO_L16` (default for streaming requests)                                                                                                                                             |
| `audioConfig.audioEncoding` : `MULAW` or `ALAW`                                        | `AUDIO_MULAW` or `AUDIO_ALAW`                                                                                                                                                            |
| `audioConfig.audioEncoding` : `MP3` or `OGG_OPUS`                                      | Not supported. Encode the audio on the client.                                                                                                                                           |
| `audioConfig.sampleRateHertz`                                                          | Not supported. For output sample rates, see [Audio output formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#audio-output-formats) . |

The Cloud Text-to-Speech API returns base64-encoded audio in `audioContent` . The Gemini Enterprise API returns it in `candidates[0].content.parts[0].inlineData.data` .

## What's next

- Try the samples in the [Gemini TTS overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .
- Learn how to direct style and vocal sounds in the [prompting guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide) .
