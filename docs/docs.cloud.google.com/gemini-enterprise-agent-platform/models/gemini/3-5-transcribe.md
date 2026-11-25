---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe
title: Gemini 3.5 Transcribe
description: Learn about Gemini 3.5 Transcribe, our model optimized for high-accuracy speech-to-text, live transcription, and automatic language identification.
data_source: docs.cloud.google.com
---

Gemini 3.5 Transcribe is Google's model for converting speech to text in multiple languages, available through Agent Platform. Based on Gemini's audio understanding capabilities, it provides low-latency, accurate transcription with utterance-based language detection, speaker diarization, word-level timestamps, [Smart transcription](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe#transcription-modes) , and custom vocabulary speech biasing.

Gemini 3.5 Transcribe serves as the primary audio transcription workhorse, bridging the gap between deep-reasoning multi-modal models and highly optimized speech-to-text workflows.

To get started, view the [introductory notebook for Gemini 3.5 Transcribe](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_5_transcribe.ipynb) .

It supports two primary methods of operation:

- **Streaming (Live) transcription** : Streams audio and receives transcription results incrementally, in real time, using the `gemini-3.5-transcribe-live` model.
- **Synchronous transcription** : Transcribes complete, prerecorded audio files in a single request using the `gemini-3.5-transcribe` model.

## Feature support and limitations

Gemini 3.5 Transcribe supports the following features across its two endpoints:

| Feature                             | Live Streaming ( `gemini-3.5-transcribe-live` )      | Audio File Processing ( `gemini-3.5-transcribe` ) | Launch Stage | Notes / Limitations                                                                                                                                                                                                                                   |
|-------------------------------------|------------------------------------------------------|---------------------------------------------------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Language Auto-detection**         | Supported (85+ languages)                            | Supported (85+ languages)                         | Supported    | Includes mid-session code-mixing.                                                                                                                                                                                                                     |
| **Utterance-level Timestamps**      | Supported                                            | Not Supported                                     | Supported    |                                                                                                                                                                                                                                                       |
| **Word-level Timestamps**           | Not Supported                                        | Supported                                         | Experimental | Degrades transcription accuracy.                                                                                                                                                                                                                      |
| **Custom Vocabulary Biasing**       | Supported (up to 1000 terms)                         | Supported (up to 1000 terms)                      | Supported    | Customers typically see best results with up to 100 terms.                                                                                                                                                                                            |
| **Smart Dictation & Formatting**    | Supported (with manual endpointing)                  | Supported                                         | Experimental | Includes filler word removal and intent-aware alphanumeric formatting. For live streaming, use with [manual endpointing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe#smart-live-manual-endpointing) . |
| **Endpointing Sensitivity Levels**  | Supported                                            | Not Supported                                     | Supported    | Controls [start-of-speech and end-of-speech sensitivity](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe#sensitivity_levels) for automatic Voice Activity Detection (VAD).                                |
| **Speaker Diarization**             | Not Supported                                        | Supported (up to 8 speakers)                      | Experimental | Attribution for 3+ speakers is Experimental.                                                                                                                                                                                                          |
| **Max Audio Duration**              | Up to 10 minutes                                     | Up to 15 minutes                                  | Supported    | File processing is limited to 15 minutes when features like diarization or timestamps are enabled.                                                                                                                                                    |
| **Voice Editing ( `source_text` )** | Supported (with `SMART` mode and manual endpointing) | Supported (with `SMART` mode)                     | Experimental | Enabled by default when `mode="SMART"` . Accepts up to 64 KB of existing `source_text` to edit, rewrite, or reformat using spoken instructions. Incompatible with word-level timestamps and speaker diarization.                                      |

## Transcription modes

Gemini 3.5 Transcribe supports two transcription modes through the `mode` parameter in `AudioTranscriptionConfig` :

- **`VERBATIM` (default)** : Returns an exact word-for-word transcript of everything spoken, preserving raw filler words ("um", "uh", "like", "you know"), repetitions, pauses, and false starts.
- **`SMART` (Smart transcription)** : Optimizes the transcript for reading by applying intelligent post-processing:
  - **Disfluency removal** : Strips conversational filler words, stuttering, and false starts.
  - **Inline self-corrections** : Resolves spoken corrections directly (for example, *"Let's meet on Tuesday, actually no, Wednesday at two"* becomes *"Let's meet on Wednesday at 2:00 PM"* ).
  - **Automatic structured formatting** : Automatically structures spoken thoughts into paragraphs, numbered lists, bullet points, formatted dates, currencies, and numbers.
  - **Grammatical cleanup** : Applies natural punctuation, sentence casing, and flow.

| Spoken audio                                                                               | `VERBATIM` output                                                                    | `SMART` (Smart transcription) output                       |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------|
| "Um, so for the meeting, I think we should, uh, invite Alice and, wait no, Bob and Carol." | "Um so for the meeting I think we should uh invite Alice and wait no Bob and Carol." | "For the meeting, I think we should invite Bob and Carol." |
| "First item review budget second item finalize timeline third item send recap"             | "first item review budget second item finalize timeline third item send recap"       | "1. Review budget 2. Finalize timeline 3. Send recap"      |

> **Note:** Smart transcription ( `SMART` ) is incompatible with `word_timestamp` and `diarization` . If you need word-level timestamps or speaker diarization, use `VERBATIM` mode.

## Live streaming transcription

The `BidiGenerateContent (Live) API` stays open while you stream small chunks of audio to the model and receive transcription results incrementally, as they become available. This is used for near real-time captioning or transcribing microphone input.

To try streaming transcription without writing any code, open `gemini-3.5-transcribe-live` on the Gemini Live API page of Agent Studio, then record or upload audio and watch the transcript stream back.

To transcribe streaming audio, build a `LiveConnectConfig` and set the `response_modalities` to `["TEXT"]` alongside your `input_audio_transcription` configuration.

```
import asyncio
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

config = types.LiveConnectConfig(
    response_modalities=["TEXT"],
    input_audio_transcription=types.AudioTranscriptionConfig(
        language_codes=["it-IT", "en-US"],
    ),
)

async def streaming_main(audio_file, config):
    # Connect to the Live API session
    async with client.aio.live.connect(model="gemini-3.5-transcribe-live", config=config) as session:
        # In a complete implementation, you would chunk the audio and send via:
        # await session.send_realtime_input(audio=types.Blob(data=data, mime_type="audio/pcm;rate=16000"))
        # await session.send_realtime_input(audio_stream_end=True)

        async for message in session.receive():
            if message.server_content:
                server_content = message.server_content

                # Track the active interim segment
                interim = server_content.interim_input_transcription
                if interim and interim.text:
                    print(f"Interim: {interim.text}")

                # Save final transcript and clear the interim
                final = server_content.input_transcription
                if final and final.text:
                    print(f"Final: {final.text}")
```

> **Note:** When establishing a Gemini Live API connection, clients must wait to receive the `setup_complete` message from the server before streaming audio data. Sending audio requests before `setup_complete` is received can cause the session to cancel unexpectedly and may result in empty transcriptions, particularly on short audio clips.

### Adjust endpointing sensitivity

Agent Platform lets you control the trade-off between latency and accuracy for streaming and real-time applications with `gemini-3.5-transcribe-live` . By default, the recognition model uses automatic Voice Activity Detection (VAD) and waits for a brief period of silence after detecting speech before committing the final `input_transcription` segment. This helps make sure that a user has finished a complete sentence or phrase, maximizing accuracy at the cost of a small delay in the final response.

You can adjust `start_of_speech_sensitivity` , `end_of_speech_sensitivity` , `prefix_padding_ms` , and `silence_duration_ms` in `AutomaticActivityDetection` for time-sensitive applications—such as voice commands or voice bots—to detect speech onset, filter out background noise, or finalize transcripts more quickly. (If you need client-controlled turn boundaries instead of automatic VAD, use [manual endpointing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe#smart-live-manual-endpointing) .) Sensitivity levels apply only to live streaming transcription ( `gemini-3.5-transcribe-live` ) when you use automatic VAD, and aren't supported for synchronous audio file processing ( `gemini-3.5-transcribe` ).

> **Note:** If the user pauses briefly while speaking, increasing end-of-speech sensitivity or lowering `silence_duration_ms` to minimize latency might result in the system "cutting off" a user and committing the transcript early.

### Sensitivity levels

When you use automatic VAD in `RealtimeInputConfig` , you can configure the following parameters in `AutomaticActivityDetection` based on your use case:

- **Start-of-speech sensitivity ( `start_of_speech_sensitivity` )** : Controls how readily the model detects the start of speech.
  - `START_SENSITIVITY_UNSPECIFIED` : Uses the default start-of-speech sensitivity.
  - `START_SENSITIVITY_HIGH` : Detects the start of speech more often. Optimized for capturing quiet speech or brief utterances, such as single-word commands, as quickly as possible. This setting might increase false triggers in noisy environments.
  - `START_SENSITIVITY_LOW` : Detects the start of speech less often. Optimized for noisy environments to reduce false triggers from background sounds.
- **End-of-speech sensitivity ( `end_of_speech_sensitivity` )** : Controls how quickly the model ends detected speech and commits the final transcript.
  - `END_SENSITIVITY_UNSPECIFIED` : Uses the default end-of-speech sensitivity.
  - `END_SENSITIVITY_HIGH` : Ends detected speech more often. Optimized for short utterances, such as single sentences or commands like "Remind me to call the dentist tomorrow". This setting reduces the wait time after speech stops, providing a faster response while maintaining reasonable sentence-level accuracy.
  - `END_SENSITIVITY_LOW` : Ends detected speech less often. Optimized for long-form dictation and speakers who take longer pauses between phrases, helping prevent premature utterance cutoffs at the cost of higher latency.
- **Prefix padding ( `prefix_padding_ms` )** : The required duration of detected speech (in milliseconds) before the model commits start-of-speech. Lower values capture brief utterances faster, while higher values help filter out short noise spikes such as clicks or pops.
- **Silence duration ( `silence_duration_ms` )** : The required duration of continuous silence (in milliseconds) before the model commits end-of-speech. Lower values finalize transcripts faster after speech stops, while higher values allow longer natural pauses mid-sentence without splitting the utterance.

```
import asyncio
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

config = types.LiveConnectConfig(
    response_modalities=["TEXT"],
    realtime_input_config=types.RealtimeInputConfig(
        automatic_activity_detection=types.AutomaticActivityDetection(
            start_of_speech_sensitivity=types.StartSensitivity.START_SENSITIVITY_LOW,
            end_of_speech_sensitivity=types.EndSensitivity.END_SENSITIVITY_HIGH,
            prefix_padding_ms=200,
            silence_duration_ms=500,
        ),
    ),
    input_audio_transcription=types.AudioTranscriptionConfig(
        language_codes=["en-US"],
    ),
)

async def streaming_with_sensitivity(audio_file, config):
    # Connect to the Live API session
    async with client.aio.live.connect(
        model="gemini-3.5-transcribe-live", config=config
    ) as session:
        # In a complete implementation, you would chunk the audio and send via:
        # await session.send_realtime_input(
        #     audio=types.Blob(data=data, mime_type="audio/pcm;rate=16000")
        # )
        # await session.send_realtime_input(audio_stream_end=True)

        async for message in session.receive():
            if message.server_content:
                server_content = message.server_content

                # Track the active interim segment
                interim = server_content.interim_input_transcription
                if interim and interim.text:
                    print(f"Interim: {interim.text}")

                # Save final transcript and clear the interim
                final = server_content.input_transcription
                if final and final.text:
                    print(f"Final: {final.text}")
```

### Live transcription with `SMART` mode and manual endpointing

When using `SMART` mode with live streaming transcription ( `gemini-3.5-transcribe-live` ), you should use **manual endpointing** (manual Voice Activity Detection) instead of automatic VAD. Because `SMART` mode applies utterance-level post-processing—such as resolving inline self-corrections and structuring lists or paragraphs—automatic VAD may prematurely split a user's thought during natural pauses.

To configure manual endpointing, disable `automatic_activity_detection` in `RealtimeInputConfig` and explicitly mark the beginning and end of the user's speech turn using `activity_start` and `activity_end` :

```
config = types.LiveConnectConfig(
    response_modalities=["TEXT"],
    realtime_input_config=types.RealtimeInputConfig(
        automatic_activity_detection=types.AutomaticActivityDetection(
            disabled=True,
        ),
    ),
    input_audio_transcription=types.AudioTranscriptionConfig(
        mode="SMART",
    ),
)

async with client.aio.live.connect(
    model="gemini-3.5-transcribe-live", config=config
) as session:
    # Signal start of speech turn
    await session.send_realtime_input(activity_start=types.ActivityStart())

    # Stream audio chunks...
    await session.send_realtime_input(
        audio=types.Blob(data=audio_bytes, mime_type="audio/pcm;rate=16000")
    )

    # Signal end of speech turn so SMART mode can process the complete utterance
    await session.send_realtime_input(activity_end=types.ActivityEnd())
```

### Live voice editing

When using `gemini-3.5-transcribe-live` with `mode="SMART"` and manual endpointing ( `automatic_activity_detection.disabled=True` ), voice editing is active across every turn in the session:

- **Empty start** : Omit `source_text` from the `LiveConnectConfig` field, to dictate from a blank state. Subsequent spoken corrections or formatting commands automatically edit the accumulated session transcript.
- **Seeded start** : Pass initial `source_text` (up to 64 KB) in `input_audio_transcription` during session setup so the first spoken turn immediately edits pre-existing text.
- **Stateful progression** : Unlike synchronous requests, the Live session retains the latest finalized `input_transcription` as the active text context for the next turn—you do not need to resend `source_text` between turns. If the user manually edits the text buffer using a keyboard between voice turns, close the current session and open a new session seeded with the updated buffer in `source_text` .

```
import asyncio
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

config = types.LiveConnectConfig(
    response_modalities=["TEXT"],
    realtime_input_config=types.RealtimeInputConfig(
        automatic_activity_detection=types.AutomaticActivityDetection(
            disabled=True,
        ),
    ),
    input_audio_transcription=types.AudioTranscriptionConfig(
        mode="SMART",
        source_text="Draft agenda: 1. Q3 metrics 2. Hiring plan",
    ),
)

async def live_voice_edit(audio_bytes: bytes):
    async with client.aio.live.connect(
        model="gemini-3.5-transcribe-live",
        config=config,
    ) as session:
        # Signal start of spoken edit command
        await session.send_realtime_input(activity_start=types.ActivityStart())

        # Stream 16kHz mono PCM audio chunks
        await session.send_realtime_input(
            audio=types.Blob(data=audio_bytes, mime_type="audio/pcm;rate=16000")
        )

        # Signal end of utterance so SMART mode finalizes the edited text
        await session.send_realtime_input(activity_end=types.ActivityEnd())

        async for message in session.receive():
            if message.server_content and message.server_content.input_transcription:
                # Contains the full updated text after applying the voice edit
                print(f"Updated text: {message.server_content.input_transcription.text}")
```

## Synchronous transcription

You can use the standard `generate_content` method to transcribe complete audio files that have already been recorded. Configure the parameters by building an `AudioTranscriptionConfig` inside `GenerateContentConfig` .

### Word-level timestamps

Setting `word_timestamp=True` returns word-level timing. The response's `audio_transcription.words` list contains each recognized word along with its `start_offset` and `end_offset` .

```
from google import genai
from google.genai import types

# Initialize the client
client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

with open("input.wav", "rb") as f:
    audio_bytes = f.read()

response = client.models.generate_content(
    model="gemini-3.5-transcribe",
    contents=[
        types.Part.from_bytes(
            data=audio_bytes,
            mime_type="audio/wav",
        ),
    ],
    config=types.GenerateContentConfig(
        audio_transcription_config=types.AudioTranscriptionConfig(
            word_timestamp=True,
        ),
    ),
)

parts = getattr(response, "parts", []) or []
if parts and (audio_tx := getattr(parts[0], "audio_transcription", None)):
    for w in getattr(audio_tx, "words", []) or []:
        print(f"[{w.start_offset} - {w.end_offset}] {w.word}")

if text := "".join(p.text for p in parts if getattr(p, "text", None)):
    print(f"**{text}**")
```

### Speaker diarization and custom vocabulary

Setting `diarization=True` asks the model to identify and label individual speakers. You can also supply a `custom_vocabulary` field with a list of phrases that bias `Gemini 3.5 Transcribe` toward recognizing specific terms. The model generally follows custom vocabulary instructions more reliably when a language is also specified using `language_codes` .

```
response = client.models.generate_content(
    model="gemini-3.5-transcribe",
    contents=[
        types.Part.from_uri(
            file_uri="gs://cloud-samples-data/generative-ai/audio/coffee_order.wav",
            mime_type="audio/wav",
        ),
    ],
    config=types.GenerateContentConfig(
        audio_transcription_config=types.AudioTranscriptionConfig(
            diarization=True,
            language_codes=["en-US"],
            custom_vocabulary=["oatmilk", "oz"],
        ),
    ),
)

parts = getattr(response, "parts", []) or []
for p in parts:
    audio_tx = getattr(p, "audio_transcription", None)
    speaker = getattr(audio_tx, "speaker_label", "UNKNOWN") if audio_tx else "UNKNOWN"
    text = getattr(p, "text", "") or (getattr(audio_tx, "text", "") if audio_tx else "")

    if text:
        print(f"**{speaker}**: {text}")
```

### Synchronous transcription with `SMART` mode

```
response = client.models.generate_content(
    model="gemini-3.5-transcribe",
    contents=[
        types.Part.from_bytes(
            data=audio_bytes,
            mime_type="audio/wav",
        ),
    ],
    config=types.GenerateContentConfig(
        audio_transcription_config=types.AudioTranscriptionConfig(
            mode="SMART",
        ),
    ),
)
```

### Synchronous voice editing

Voice editing is enabled by default whenever `mode="SMART"` is set. In addition to cleaning up spoken disfluencies and inline self-corrections during fresh dictation, you can pass existing text in `source_text` (up to 64 KB) so the model applies spoken editing, rewriting, or formatting instructions directly to that draft.

Rather than returning a diff, `gemini-3.5-transcribe` returns the complete updated text in `response.text` . Because `generate_content` requests are stateless, implement multi-turn voice editing by passing the previous turn's output back as `source_text` on the next request:

```
from google import genai
from google.genai import types

client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

current_text = "The project sync is scheduled for Tuesday at 2 PM in Room 4B."

with open("edit_instruction.wav", "rb") as f:
    audio_bytes = f.read()

# Example spoken audio: "Change Tuesday to Wednesday and make it sound more formal."
response = client.models.generate_content(
    model="gemini-3.5-transcribe",
    contents=[
        types.Part.from_bytes(
            data=audio_bytes,
            mime_type="audio/wav",
        ),
    ],
    config=types.GenerateContentConfig(
        audio_transcription_config=types.AudioTranscriptionConfig(
            mode="SMART",
            source_text=current_text,
        ),
    ),
)

updated_text = response.text
print(updated_text)
```

## Language support

The following languages and BCP-47 language codes are supported for Gemini 3.5 Transcribe:

| Language                | BCP-47 Code   | Readiness    | Language                      | BCP-47 Code   | Readiness    |
|-------------------------|---------------|--------------|-------------------------------|---------------|--------------|
| Afrikaans               | `af-ZA`       | Experimental | Japanese                      | `ja-JP`       | Supported    |
| Amharic                 | `am-ET`       | Experimental | Javanese                      | `jv-ID`       | Experimental |
| Arabic (Egypt)          | `ar-EG`       | Experimental | Kabuverdianu                  | `kea-CV`      | Experimental |
| Armenian                | `hy-AM`       | Experimental | Kannada                       | `kn-IN`       | Experimental |
| Assamese                | `as-IN`       | Experimental | Kazakh                        | `kk-KZ`       | Experimental |
| Azerbaijani             | `az-AZ`       | Experimental | Korean                        | `ko-KR`       | Supported    |
| Belarusian              | `be-BY`       | Experimental | Kyrgyz                        | `ky-KG`       | Experimental |
| Bengali (Bangladesh)    | `bn-BD`       | Experimental | Latvian                       | `lv-LV`       | Experimental |
| Bengali (India)         | `bn-IN`       | Experimental | Lingala                       | `ln-CD`       | Experimental |
| Bosnian                 | `bs-BA`       | Experimental | Lithuanian                    | `lt-LT`       | Experimental |
| Bulgarian               | `bg-BG`       | Experimental | Macedonian                    | `mk-MK`       | Experimental |
| Bulgarian (Aromanian)   | `rup-BG`      | Experimental | Malay                         | `ms-MY`       | Experimental |
| Burmese                 | `my-MM`       | Experimental | Malayalam                     | `ml-IN`       | Experimental |
| Cantonese (Traditional) | `yue-Hant-HK` | Experimental | Maltese                       | `mt-MT`       | Experimental |
| Catalan                 | `ca-ES`       | Supported    | Mandarin Chinese (Simplified) | `cmn-Hans-CN` | Supported    |
| Cebuano                 | `ceb`         | Experimental | Marathi                       | `mr-IN`       | Experimental |
| Central Khmer           | `km-KH`       | Experimental | Mongolian                     | `mn-MN`       | Experimental |
| Croatian                | `hr-HR`       | Supported    | Nepali                        | `ne-NP`       | Experimental |
| Czech                   | `cs-CZ`       | Experimental | Norwegian                     | `nb-NO`       | Experimental |
| Danish                  | `da-DK`       | Supported    | Oriya                         | `or-IN`       | Experimental |
| Dutch                   | `nl-NL`       | Supported    | Polish                        | `pl-PL`       | Supported    |
| English (Australia)     | `en-AU`       | Supported    | Portuguese (Brazil)           | `pt-BR`       | Supported    |
| English (Great Britain) | `en-GB`       | Supported    | Portuguese (Portugal)         | `pt-PT`       | Supported    |
| English (India)         | `en-IN`       | Supported    | Punjabi                       | `pa-IN`       | Experimental |
| English (United States) | `en-US`       | Supported    | Punjabi (Gurmukhi script)     | `pa-Guru-IN`  | Experimental |
| Estonian                | `et-EE`       | Experimental | Romanian                      | `ro-RO`       | Supported    |
| Farsi                   | `fa-IR`       | Experimental | Russian                       | `ru-RU`       | Supported    |
| Filipino                | `fil-PH`      | Experimental | Serbian                       | `sr-RS`       | Experimental |
| Finnish                 | `fi-FI`       | Supported    | Sindhi (Arabic script)        | `sd-Arab-IN`  | Experimental |
| French                  | `fr-FR`       | Supported    | Slovak                        | `sk-SK`       | Experimental |
| French (Canada)         | `fr-CA`       | Supported    | Slovenian                     | `sl-SI`       | Experimental |
| Galician                | `gl-ES`       | Experimental | Spanish (Latin America)       | `es-419`      | Experimental |
| Georgian                | `ka-GE`       | Experimental | Spanish (Spain)               | `es-ES`       | Supported    |
| German                  | `de-DE`       | Supported    | Spanish (United States)       | `es-US`       | Supported    |
| Greek                   | `el-GR`       | Supported    | Swahili (Kenya)               | `sw-KE`       | Experimental |
| Gujarati                | `gu-IN`       | Experimental | Swedish                       | `sv-SE`       | Supported    |
| Hausa                   | `ha-NG`       | Experimental | Tajik                         | `tg-TJ`       | Experimental |
| Hebrew                  | `he-IL`       | Experimental | Telugu                        | `te-IN`       | Experimental |
| Hindi                   | `hi-IN`       | Supported    | Thai                          | `th-TH`       | Experimental |
| Hungarian               | `hu-HU`       | Experimental | Turkish                       | `tr-TR`       | Supported    |
| Icelandic               | `is-IS`       | Experimental | Ukrainian                     | `uk-UA`       | Supported    |
| Indonesian              | `id-ID`       | Experimental | Uzbek                         | `uz-UZ`       | Experimental |
| Italian                 | `it-IT`       | Supported    | Vietnamese                    | `vi-VN`       | Supported    |

## Regional availability

Gemini 3.5 Transcribe is available in the following Google Cloud locations:

| Endpoint                     | Google Cloud Location | Launch Readiness |
|------------------------------|-----------------------|------------------|
| `gemini-3.5-transcribe`      | `global`              | Supported        |
| `gemini-3.5-transcribe`      | `us`                  | Supported        |
| `gemini-3.5-transcribe`      | `eu`                  | Supported        |
| `gemini-3.5-transcribe-live` | `global`              | Supported        |
| `gemini-3.5-transcribe-live` | `us`                  | Supported        |
| `gemini-3.5-transcribe-live` | `eu`                  | Supported        |

## Best practices

- **Provide clean audio** : Ensure audio recordings have clear voice separation and avoid severe clipping.
- **Provide language hints when known** : If you know the audio language in advance, specify `language_codes` to maximize accuracy.
- **Target custom vocabulary** : Include only distinct domain terms, brand names, or proper nouns in `custom_vocabulary` rather than common everyday words.
- **Use manual endpointing with `SMART` mode in live transcription** : Disable automatic VAD ( `automatic_activity_detection` ) and explicitly send `activity_start` and `activity_end` signals so the model can apply disfluency removal, self-corrections, and formatting across complete utterances.

[Try in Agent Studio](https://console.cloud.google.com/agent-platform/studio/multimodal-live?model=gemini-3.5-transcribe-live) [Pricing](https://cloud.google.com/model-garden/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<td><code>['gemini-3.5-transcribe', 'gemini-3.5-transcribe-live']</code></td>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<td>description
Text<br />
Output only
hide_image
Image<br />
Not supported
mic
Audio<br />
Input only
videocam_off
Video<br />
Not supported</td>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/thinking">Thinking</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instruction-introduction">System instructions</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/control-generated-output">Structured output</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview">Context caching</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/rag-engine/rag-overview">RAG Engine</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tuning">Tuning</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/video-understanding#agentic-video-processing">Agentic video understanding</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Tools</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/overview">Grounding</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution">Code execution</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling">Function calling</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/url-context">URL context</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/computer-use">Computer use</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>APIs</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Consumption options</th>
<td><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput">Provisioned Throughput</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/batch-inference">Batch inference</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Standard PayGo<br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier">Deferred tier</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas">Fixed quota</a><br />
Not supported</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Supported regions</th>
<td><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></td>
<td><ul>
<li>Global: <code>global</code></li>
<li>Multi-region: <code>us</code> , <code>eu</code></li>
</ul></td>
</tr>
<tr class="even">
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency">ML processing</a></strong></p></th>
<td><ul>
<li>United States: <code>Multi-region</code></li>
<li>Europe: <code>Multi-region</code></li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<th>Versions</th>
<td><ul>
<li><code>gemini-3.5-transcribe-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: August 2026</li>
</ul></li>
<li><code>gemini-3.5-transcribe</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: October 2026</li>
</ul></li>
<li><code>gemini-3.5-transcribe-live-preview</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: August 2026</li>
</ul></li>
<li><code>gemini-3.5-transcribe-live</code>
<ul>
<li>Launch stage: GA</li>
<li>Release date: October 2026</li>
</ul></li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<th>Security controls</th>
<td><strong>Online prediction</strong></td>
<td><ul>
<li>Data residency</li>
<li>CMEK</li>
<li>VPC-SC</li>
<li>AXT</li>
</ul></td>
</tr>
<tr class="odd">
<th>See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls">Security controls</a> for more information.</th>
<td></td>
<td></td>
</tr>
</tbody>
</table>
