---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-language-voice
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-language-voice
title: Configure language and voice
description: Configure `SpeechConfig` language, `VoiceConfig` options, and `AutomaticActivityDetection` for real-time synthesized speech interactions.
data_source: docs.cloud.google.com
---

This document describes how to configure synthesized speech responses and voice activity detection in Gemini Live API. You can configure responses in a variety of HD voices and languages, and also configure voice activity detection settings to allow users to interrupt the model.

## Set the language and voice

Live audio models like `gemini-3.8-live` can switch between languages naturally during conversation. You can also restrict the languages it speaks in by specifying it in the system instructions.

Voice is configured in the `voice_name` field for all models.

The following code sample shows you how to configure language and voice.

    from google.genai.types import LiveConnectConfig, SpeechConfig, VoiceConfig, PrebuiltVoiceConfig
    
    config = LiveConnectConfig(
      response_modalities=["AUDIO"],
      speech_config=SpeechConfig(
        voice_config=VoiceConfig(
            prebuilt_voice_config=PrebuiltVoiceConfig(
                voice_name=voice_name,
            )
        ),
        language_code="en-US",
      ),
    )

> **Tip:** For the best results when prompting and requiring the model to respond in a non-English language, include the following as part of your system instructions:
> 
> ``` 
> RESPOND IN LANGUAGE. YOU MUST RESPOND UNMISTAKABLY IN LANGUAGE.
>     
> ```

## Guide voice tone and accent

You can guide the voice's tone and accent using system instructions, and Gemini Live API responds with the voice you instructed. For example, "English with a positive upbeat voice with a French accent." For more information, see [Gemini Live API prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/live-api-prompt-guide) .

## Voices supported

Gemini Live API supports the following 30 voice options in the `voice_name` field:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Zephyr -- <em>Bright</em><br />
Kore -- <em>Firm</em><br />
Orus -- <em>Firm</em><br />
Autonoe -- <em>Bright</em><br />
Umbriel -- <em>Easy-going</em><br />
Erinome -- <em>Clear</em><br />
Laomedeia -- <em>Upbeat</em><br />
Schedar -- <em>Even</em><br />
Achird -- <em>Friendly</em><br />
Sadachbia -- <em>Lively</em></td>
<td>Puck -- <em>Upbeat</em><br />
Fenrir -- <em>Excitable</em><br />
Aoede -- <em>Breezy</em><br />
Enceladus -- <em>Breathy</em><br />
Algieba -- <em>Smooth</em><br />
Algenib -- <em>Gravelly</em><br />
Achernar -- <em>Soft</em><br />
Gacrux -- <em>Mature</em><br />
Zubenelgenubi -- <em>Casual</em><br />
Sadaltager -- <em>Knowledgeable</em></td>
<td>Charon -- <em>Informative</em><br />
Leda -- <em>Youthful</em><br />
Callirrhoe -- <em>Easy-going</em><br />
Iapetus -- <em>Clear</em><br />
Despina -- <em>Smooth</em><br />
Rasalgethi -- <em>Informative</em><br />
Alnilam -- <em>Firm</em><br />
Pulcherrima -- <em>Forward</em><br />
Vindemiatrix -- <em>Gentle</em><br />
Sulafat -- <em>Warm</em></td>
</tr>
</tbody>
</table>

### Languages supported

Gemini Live API supports the following languages:

| Language               | BCP-47 Code          |
| :--------------------- | :------------------- |
| Arabic (Egyptian)      | ar-EG                |
| Bengali (Bangladesh)   | bn-BD                |
| Dutch (Netherlands)    | nl-NL                |
| English (India)        | en-IN & hi-IN bundle |
| English (US)           | en-US                |
| French (France)        | fr-FR                |
| German (Germany)       | de-DE                |
| Hindi (India)          | hi-IN                |
| Indonesian (Indonesia) | id-ID                |
| Italian (Italy)        | it-IT                |
| Japanese (Japan)       | ja-JP                |
| Korean (Korea)         | ko-KR                |
| Marathi (India)        | mr-IN                |
| Polish (Poland)        | pl-PL                |
| Portuguese (Brazil)    | pt-BR                |
| Romanian (Romania)     | ro-RO                |
| Russian (Russia)       | ru-RU                |
| Spanish (US)           | es-US                |
| Tamil (India)          | ta-IN                |
| Telugu (India)         | te-IN                |
| Thai (Thailand)        | th-TH                |
| Turkish (Turkey)       | tr-TR                |
| Ukrainian (Ukraine)    | uk-UA                |
| Vietnamese (Vietnam)   | vi-VN                |

## Use a custom voice

Instead of a prebuilt voice, you can provide a short recording of a voice that Gemini Live API replicates in synthesized speech responses. Custom voices are configured per session in the `replicated_voice_config` field of `voice_config` . There's nothing to upload or train in advance.

> Custom voices are only available to select customers. To request access, reach out to your Google Cloud account team. You are responsible for securing all consents and rights necessary for the processing of face and/or voice samples. When using this feature, you must comply with the [GenAI Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) , the [Google Cloud Acceptable Use Policy](https://cloud.google.com/terms/aup?e=48754805) , and the agreement under which you access and use Google Cloud services, including Section 32 of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) .

### Voice sample requirements

The voice sample must meet the following specifications:

  - **Audio format** : PCM audio `s16le` with variable sample rate, for example `audio/pcm;rate=24000`

  - **Duration** : 10 to 20 seconds.

### Recording a custom voice

When recording the voice sample, we recommend the following tips for the best voice quality:

1.  **Speak naturally** : Don't use a "radio voice" or over-enunciate unless you want the avatar to sound like a broadcaster. Read the script exactly as if you would speak to a friend.

2.  **Limit background noise** : Limit the background noise as much as possible: turn off fans, turn off AC units, and close any open windows.

3.  **Smile slightly** : Smiling while recording tends to cause you to add warmth to the recording, and that warmth is then added to the replicated voice.

#### Custom voice recommended scripts

We recommend that you use one of the following scripts to record custom voices:

  - **Phonetic standard, best for overall quality** : "When the sunlight strikes raindrops in the air, they act like a prism and form a rainbow. The rainbow is a division of white light into many beautiful colors. These take the shape of a long round arch."

  - **Storyteller, best for capturing emotion and dynamic range** : "I couldn't believe my eyes when I opened the dusty, old book. A small golden key clattered onto the wooden floor. 'Where did this come from?' I whispered to myself, feeling a sudden thrill of excitement. Everything was about to change."

### Set the custom voice

Configure the custom voice in the initial `setup` payload that you send over the WebSocket connection:

    import base64
    import json
    import websockets
    
    # Load custom voice audio (PCM s16le, e.g., 24kHz)
    with open("/path/to/your/audio_sample.wav", "rb") as f:
        wav_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    # Setup generation config with custom voice
    GENERATION_CONFIG = {
        "response_modalities": ["AUDIO"],
        "speech_config": {
            "voice_config": {
                "replicated_voice_config": {
                    "voice_sample_audio": "VOICE_SAMPLE",
                    "mime_type": "VOICE_MIME_TYPEaudio/pcm;rate=24000",
                }
            }
        },
    }
    
    # Session setup message
    SETUP_MESSAGE = {
        "setup": {
            "model": "gemini-3.8-live",
            "generation_config": GENERATION_CONFIG,
            "system_instruction": {
                "parts": [{"text": "Your system instruction here"}]
            },
            "input_audio_transcription": {},
            "output_audio_transcription": {},
        }
    }

Replace the following:

  - VOICE\_SAMPLE : a base64-encoded PCM audio string (10-20s sample).

  - VOICE\_MIME\_TYPE : MIME type for PCM audio, for example `"audio/pcm;rate=24000"` .

You can pair a custom voice with a prebuilt avatar or a custom avatar. For more information, see [Configure live avatars](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars) .

## Configure voice activity detection

*Voice activity detection* (VAD) allows the model to recognize when a person is speaking. This is essential for creating natural conversations, because it allows a user to interrupt the model at any time.

When VAD detects an interruption, the ongoing generation is canceled and discarded. Only the information already sent to the client is retained in the session history. The server then sends a `BidiGenerateContentServerContent` message to report the interruption. The server then discards any pending function calls and sends a `BidiGenerateContentServerContent` message with the IDs of the canceled calls.

### Python

``` 
config = {
    "response_modalities": ["audio"],
    "realtime_input_config": {
        "automatic_activity_detection": {
            "disabled": False, # default
            "start_of_speech_sensitivity": "low",
            "end_of_speech_sensitivity": "low",
            "prefix_padding_ms": 20,
            "silence_duration_ms": 100,
        }
    }
}
      
```

## What's next

  - [Start and manage live sessions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session)
  - [Send audio and video streams](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/send-audio-video-streams)
  - [Configure Gemini capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-gemini-capabilities)
  - [Best practices with Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/best-practices)
