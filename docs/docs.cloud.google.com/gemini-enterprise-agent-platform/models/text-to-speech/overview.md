---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview
title: Generate speech with Gemini TTS
description: Learn how to generate single-speaker and multi-speaker speech from text with the Gemini 3.8 Flash TTS and Gemini 3.8 Flash-Lite TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

> To learn more, run the "Gemini 3.8 Flash TTS" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb)

The Gemini text-to-speech (TTS) models convert text into single-speaker or multi-speaker audio. You can control the *style* , *accent* , *pace* , and *tone* of the audio with structured turn metadata ( `speech_metadata` ) and inline vocal tags.

This page shows you how to generate speech with the following models using the `generateContent` and `streamGenerateContent` methods of the Gemini Enterprise API:

- [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` )
- [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` )

The TTS models are tailored for exact text recitation with fine-grained control over style and sound, such as narration, audiobooks, and voice agent responses. For interactive, real-time conversations with audio input and output, use the [Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) instead.

If you use an earlier Gemini TTS model, such as `gemini-3.1-flash-tts-preview` , see the [migration guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide) .

## Supported models

| Model                                                                                                                                                        | Single speaker | Multi-speaker | Streaming | [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) | [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------|---------------|-----------|-------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` )                |                |               |           |                                                                                                                   |                                                                                                                             |
| [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ) |                |               |           |                                                                                                                   |                                                                                                                             |
| [Gemini 3.1 Flash TTS Preview](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts#gemini-3-1-flash-tts-preview) ( `gemini-3.1-flash-tts-preview` ) |                |               |           |                                                                                                                   |                                                                                                                             |
| [Gemini 2.5 Pro TTS](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts#gemini-2-5-pro-tts) ( `gemini-2.5-pro-tts` )                               |                |               |           |                                                                                                                   |                                                                                                                             |
| [Gemini 2.5 Flash TTS](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts#gemini-2-5-flash-tts) ( `gemini-2.5-flash-tts` )                         |                |               |           |                                                                                                                   |                                                                                                                             |

The samples and features on this page apply to the Gemini 3.8 TTS models. For the earlier models, see [Gemini-TTS](https://docs.cloud.google.com/text-to-speech/docs/gemini-tts) in the Google Cloud Text-to-Speech documentation.

### When to use which model

Both Gemini 3.8 TTS models share the same request schema and prompting format, so you can switch between them by changing the model ID:

- **Use [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` )** when acoustic fidelity, nuanced acting, and expressive control are the top priority. It suits studio-grade creative work, complex multi-speaker dialogue, frequent vocal-burst tags, difficult pronunciations, regional or minority dialects, and long-form narration that needs a stable voice and room tone.
- **Use [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` )** for fast, cost-efficient production workloads. It's the recommended replacement for `gemini-3.1-flash-tts-preview` , and suits high-volume batch production, conversational voice agent cascades, read-aloud features, voice replication, and everyday single-speaker speech across major languages.

## Before you begin

1.  [Set up a project and enable the Gemini Enterprise API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start) .

2.  [Configure Application Default Credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/gcp-auth) for your development environment.

3.  To use the Python samples, install version 2.25.0 or later of the [Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries) :

    ```
    pip install --upgrade "google-genai>=2.25.0"
    ```

The Gemini 3.8 TTS models are available in the `global` location. Send requests to the `aiplatform.googleapis.com` endpoint.

## Single-speaker TTS

To convert text to single-speaker audio, pass the verbatim transcript in `parts[].text` , add optional turn-level styling in `parts[].speech_metadata` , and set the voice in `speechConfig.voiceConfig.voice` . The `voice` field accepts a [prebuilt voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#prebuilt-voices) name, an [Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library) voice ID, or the ID ( `voice_...` ) of a [designed](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) or [replicated](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) voice (or an optional stateless `voicekey_...` key).

By default, unary requests return a complete WAV file (16-bit PCM, 24 kHz, mono), so you can write the audio bytes directly to a `.wav` file. Streaming requests return raw PCM chunks instead. For details and other encodings, see [Audio output formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#audio-output-formats) .

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.8-flash-tts",
    contents=[{
        "role": "user",
        "parts": [{
            "text": "Have a wonderful day!",
            "speech_metadata": {"style": "cheerful and friendly"},
        }],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {"voice_config": {"voice": "Kore"}},
    },
)

# The SDK has already decoded the base64 audio, so inline_data.data is a
# complete WAV file by default.
with open("out.wav", "wb") as f:
    f.write(response.candidates[0].content.parts[0].inline_data.data)
```

### REST

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [{
        "text": "Have a wonderful day!",
        "speechMetadata": {"style": "cheerful and friendly"}
      }]
    }],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "voiceConfig": {"voice": "Kore"}
      }
    }
  }' | jq -r '.candidates[0].content.parts[0].inlineData.data' | base64 --decode > out.wav
```

## Single-speaker streaming TTS

To receive audio while the model is still synthesizing it, use the `streamGenerateContent` method. Streaming responses return headerless raw 16-bit PCM chunks (24 kHz, mono), so you can pass each chunk to a player, a socket, or another audio pipeline as it arrives. In the following Python sample, the `emit_audio` function stands in for that destination.

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

def emit_audio(pcm: bytes) -> None:
    """Sends a chunk of raw 16-bit PCM audio (24 kHz, mono) downstream."""
    # Replace with your audio destination, such as a player, a WebSocket,
    # or a telephony stream.
    print(f"Received {len(pcm)} bytes of audio")

response_stream = client.models.generate_content_stream(
    model="gemini-3.8-flash-lite-tts",
    contents=[{
        "role": "user",
        "parts": [{
            "text": "Have a wonderful day!",
            "speech_metadata": {"style": "cheerful and friendly"},
        }],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {"voice_config": {"voice": "Kore"}},
    },
)

for chunk in response_stream:
    if not chunk.candidates or not chunk.candidates[0].content:
        continue
    for part in chunk.candidates[0].content.parts or []:
        if part.inline_data and part.inline_data.data:
            emit_audio(part.inline_data.data)
```

### REST

```
curl -N -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-lite-tts:streamGenerateContent?alt=sse" \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [{
        "text": "Have a wonderful day!",
        "speechMetadata": {"style": "cheerful and friendly"}
      }]
    }],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "voiceConfig": {"voice": "Kore"}
      }
    }
  }' | sed -n 's/^data: //p' \
    | jq -r '.candidates[0].content.parts[0].inlineData.data // empty' \
    | while read -r chunk; do echo "$chunk" | base64 --decode; done > streamed.pcm
```

The `streamed.pcm` file contains raw 16-bit PCM audio at 24 kHz, mono.

## Multi-speaker TTS

For dialogue between two speakers, configure both speakers in `speechConfig.multiSpeakerVoiceConfig.speakerVoiceConfigs` . Then pass each turn as a separate `part` , set `speech_metadata.speaker` on every turn to one of the configured speaker names, and add an optional turn-level `style` .

Multi-speaker requests require exactly two speakers.

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.8-flash-tts",
    contents=[{
        "role": "user",
        "parts": [
            {
                "text": "How's it going today, Jane?",
                "speech_metadata": {"speaker": "Joe", "style": "cheerful and friendly"},
            },
            {
                "text": "Not too bad, how about you? Ready to test these new voices?",
                "speech_metadata": {"speaker": "Jane", "style": "calm and relaxed"},
            },
        ],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {
            "multi_speaker_voice_config": {
                "speaker_voice_configs": [
                    {"speaker": "Joe", "voice_config": {"voice": "Puck"}},
                    {"speaker": "Jane", "voice_config": {"voice": "Kore"}},
                ]
            }
        },
    },
)

with open("dialogue.wav", "wb") as f:
    f.write(response.candidates[0].content.parts[0].inline_data.data)
```

### REST

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [
        {
          "text": "How'\''s it going today, Jane?",
          "speechMetadata": {"speaker": "Joe", "style": "cheerful and friendly"}
        },
        {
          "text": "Not too bad, how about you? Ready to test these new voices?",
          "speechMetadata": {"speaker": "Jane", "style": "calm and relaxed"}
        }
      ]
    }],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "multiSpeakerVoiceConfig": {
          "speakerVoiceConfigs": [
            {"speaker": "Joe", "voiceConfig": {"voice": "Puck"}},
            {"speaker": "Jane", "voiceConfig": {"voice": "Kore"}}
          ]
        }
      }
    }
  }' | jq -r '.candidates[0].content.parts[0].inlineData.data' | base64 --decode > dialogue.wav
```

## Multi-speaker streaming TTS

Multi-speaker requests also support streaming. Use the same request as in [Multi-speaker TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#multi-speaker) with the `streamGenerateContent` method.

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

def emit_audio(pcm: bytes) -> None:
    """Sends a chunk of raw 16-bit PCM audio (24 kHz, mono) downstream."""
    # Replace with your audio destination, such as a player, a WebSocket,
    # or a telephony stream.
    print(f"Received {len(pcm)} bytes of audio")

response_stream = client.models.generate_content_stream(
    model="gemini-3.8-flash-tts",
    contents=[{
        "role": "user",
        "parts": [
            {
                "text": "How's it going today, Jane?",
                "speech_metadata": {"speaker": "Joe", "style": "cheerful and friendly"},
            },
            {
                "text": "Not too bad, how about you? Ready to test these new voices?",
                "speech_metadata": {"speaker": "Jane", "style": "calm and relaxed"},
            },
        ],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {
            "multi_speaker_voice_config": {
                "speaker_voice_configs": [
                    {"speaker": "Joe", "voice_config": {"voice": "Puck"}},
                    {"speaker": "Jane", "voice_config": {"voice": "Kore"}},
                ]
            }
        },
    },
)

for chunk in response_stream:
    if not chunk.candidates or not chunk.candidates[0].content:
        continue
    for part in chunk.candidates[0].content.parts or []:
        if part.inline_data and part.inline_data.data:
            emit_audio(part.inline_data.data)
```

### REST

```
curl -N -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:streamGenerateContent?alt=sse" \
  -d '{
    "contents": [{
      "role": "user",
      "parts": [
        {
          "text": "How'\''s it going today, Jane?",
          "speechMetadata": {"speaker": "Joe", "style": "cheerful and friendly"}
        },
        {
          "text": "Not too bad, how about you? Ready to test these new voices?",
          "speechMetadata": {"speaker": "Jane", "style": "calm and relaxed"}
        }
      ]
    }],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "speechConfig": {
        "multiSpeakerVoiceConfig": {
          "speakerVoiceConfigs": [
            {"speaker": "Joe", "voiceConfig": {"voice": "Puck"}},
            {"speaker": "Jane", "voiceConfig": {"voice": "Kore"}}
          ]
        }
      }
    }
  }' | sed -n 's/^data: //p' \
    | jq -r '.candidates[0].content.parts[0].inlineData.data // empty' \
    | while read -r chunk; do echo "$chunk" | base64 --decode; done > dialogue_streamed.pcm
```

The `dialogue_streamed.pcm` file contains raw 16-bit PCM audio at 24 kHz, mono.

## Control speech style with metadata and tags

The Gemini 3.8 TTS models treat the `text` field as a verbatim transcript. Instructions written into the text, such as `"Say cheerfully: Hello!"` or `"Speaker 1: Hello!"` , might be read aloud. To control delivery, split your instructions by scope:

- **Sustained turn-level delivery ( `speech_metadata.style` )** : Put emotion, delivery style, prosody, pacing, and volume that apply to a whole turn in `speech_metadata.style` . For example, `"style": "whispered urgently"` , `"style": "out of breath"` , or `"style": "warm and enthusiastic"` .
- **Point-in-time events (inline tags)** : Put momentary non-speech vocal sounds and pauses inside the transcript in angle brackets. For example, `"Wait... <short pause> did you hear that? <sigh>"` or `"Excuse me <cough> as I was saying..."` .

For more guidance, see the [prompting guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide) .

## Voice options

The Gemini 3.8 TTS models support four ways to select or create voices:

1.  **[Prebuilt voices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#prebuilt-voices)** : 30 curated voices.
2.  **[Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library)** : More than 2,000 curated preset voices across languages, regional accents, and character personas.
3.  **[Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design)** : Create a custom voice from a natural-language description with the Voices API `create` method ( `client.voices.create()` in the Google Gen AI SDK, or `POST https://aiplatform.googleapis.com/v1beta1/projects/ `` PROJECT_ID `` /locations/global/voices` ). Set `type` to `VOICE_TYPE_PROMPTED` and `store` to `true` . The response returns a stored `voice_...` ID and a sample of the voice.
4.  **[Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication)** : Replicate a speaker's voice from reference and consent audio with the same `create` method. Set `type` to `VOICE_TYPE_REPLICATED` . With `store: true` , the response returns a stored `voice_...` ID. With `store: false` , it returns a stateless `voicekey_...` key.

### Custom voice limits and TTL

| Voice type                                                | Storage mode   | Management                                                  | Expiration                |
|-----------------------------------------------------------|----------------|-------------------------------------------------------------|---------------------------|
| **Stored voices** ( `voice_...` , designed or replicated) | `store: true`  | Voices API `list` , `get` , and `delete` methods            | **1 year after last use** |
| **Voice replication keys** ( `voicekey_...` )             | `store: false` | Managed by your application. Google doesn't retain the key. | **7 days after creation** |

Generating speech with a stored voice restarts its one-year retention period, so a voice that you use regularly doesn't expire. Voice creation requests are subject to a per-project, per-minute quota. If you exceed it, the `create` method returns a `RESOURCE_EXHAUSTED` error. For more information, see [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas) .

### Prebuilt voices

The following list shows each prebuilt voice name and its characteristic:

- **Achernar** : Soft
- **Achird** : Friendly
- **Algenib** : Gravelly
- **Algieba** : Smooth
- **Alnilam** : Firm
- **Aoede** : Breezy
- **Autonoe** : Bright
- **Callirrhoe** : Easy-going
- **Charon** : Informative
- **Despina** : Smooth
- **Enceladus** : Breathy
- **Erinome** : Clear
- **Fenrir** : Excitable
- **Gacrux** : Mature
- **Iapetus** : Clear
- **Kore** : Firm
- **Laomedeia** : Upbeat
- **Leda** : Youthful
- **Orus** : Firm
- **Puck** : Upbeat
- **Pulcherrima** : Forward
- **Rasalgethi** : Informative
- **Sadachbia** : Lively
- **Sadaltager** : Knowledgeable
- **Schedar** : Even
- **Sulafat** : Warm
- **Umbriel** : Easy-going
- **Vindemiatrix** : Gentle
- **Zephyr** : Bright
- **Zubenelgenubi** : Casual

### Extended Voice Library

Beyond the 30 prebuilt voices, the Extended Voice Library provides more than 2,000 curated preset voices across languages, regional accents, character personas, and use cases such as audiobooks, conversational agents, and news. To use a library voice, pass its ID in `speechConfig.voiceConfig.voice` , the same way that you pass a prebuilt voice name.

To browse the library, call the Voices API `list` method ( `ListVoices` ). It returns the custom voices stored in your project, followed by the prebuilt and Extended Voice Library voices. Each library voice includes its `id` and metadata such as `language_code` , `accent` , `gender` , `pitch` , `persona` , and `description` . To narrow the results, use the following filters:

- `type` : The voice source: `prebuilt` for prebuilt and library voices, `prompted` for designed voices, or `replicated` for replicated voices. If you pass more than one value, the method returns voices that match any of them.
- `search` : Text to match, case-insensitively, against each voice's display name and description.

The following example searches the library for narrator voices:

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.voices.list(type_=["prebuilt"], search="narrator", page_size=50)
for voice in response.voices or []:
    print(voice.id, voice.language_code, voice.gender, voice.description)
```

### REST

```
curl -G \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices \
  --data-urlencode "type=prebuilt" \
  --data-urlencode "search=narrator" \
  --data-urlencode "pageSize=50"
```

The `list` method returns up to 50 voices per page. To get the next page, pass the `next_page_token` value from the response as the `page_token` parameter.

> **Note:** The `list` method doesn't support filtering on other voice metadata, such as `language_code` or `gender` . Requests that set these filters fail with an `INVALID_ARGUMENT` error.

## Audio output formats

The default audio encoding depends on the method:

- **Unary requests ( `generateContent` )** return a complete WAV file ( `audio/wav` ) with a RIFF header: 16-bit PCM, 24 kHz, mono.
- **Streaming requests ( `streamGenerateContent` )** return headerless raw 16-bit signed little-endian PCM chunks ( `audio/l16` ) at 24 kHz, mono.

To request a different encoding, set `generationConfig.responseFormat` to an audio format. The Gemini 3.8 TTS models support the following `mimeType` values:

| `mimeType` value                  | Format                     | Description                                                                                                                   |
|-----------------------------------|----------------------------|-------------------------------------------------------------------------------------------------------------------------------|
| `AUDIO_WAV` *(unary default)*     | WAV ( `audio/wav` )        | Complete WAV file with a RIFF header (16-bit PCM, 24 kHz, mono).                                                              |
| `AUDIO_L16` *(streaming default)* | Linear PCM ( `audio/l16` ) | Headerless raw 16-bit signed little-endian PCM. Use for streaming, custom audio pipelines, or concatenating multi-turn clips. |
| `AUDIO_MULAW`                     | μ-law ( `audio/mulaw` )    | G.711 μ-law companded audio (8 kHz, mono), commonly used in North American and Japanese telephony.                            |
| `AUDIO_ALAW`                      | A-law ( `audio/alaw` )     | G.711 A-law companded audio (8 kHz, mono), commonly used in European and international telephony.                             |

The models ignore the `sampleRate` field. Linear PCM and WAV output is 24 kHz, and μ-law and A-law output is 8 kHz, regardless of the rate in the response `mimeType` . Resample the output on the client if your pipeline requires a different sample rate.

The following example requests μ-law output for a telephony pipeline. The Google Gen AI SDK for Python doesn't expose `responseFormat` in `GenerateContentConfig` , so the Python sample passes it in the request body with `http_options.extra_body` .

### Python

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.8-flash-tts",
    contents=[{"role": "user", "parts": [{"text": "Have a wonderful day!"}]}],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {"voice_config": {"voice": "Kore"}},
        "http_options": {
            "extra_body": {
                "generationConfig": {
                    "responseFormat": [{"audio": {"mimeType": "AUDIO_MULAW"}}]
                }
            }
        },
    },
)

# The response is headerless μ-law audio at 8 kHz, mono.
with open("out.mulaw", "wb") as f:
    f.write(response.candidates[0].content.parts[0].inline_data.data)
```

### REST

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent \
  -d '{
    "contents": [{"role": "user", "parts": [{"text": "Have a wonderful day!"}]}],
    "generationConfig": {
      "responseModalities": ["AUDIO"],
      "responseFormat": [{"audio": {"mimeType": "AUDIO_MULAW"}}],
      "speechConfig": {
        "voiceConfig": {"voice": "Kore"}
      }
    }
  }' | jq -r '.candidates[0].content.parts[0].inlineData.data' | base64 --decode > out.mulaw
```

## Supported languages

The Gemini 3.8 TTS models detect the input language automatically. Gemini 3.8 Flash TTS supports 130 languages, and Gemini 3.8 Flash-Lite TTS supports 101 languages:

| Language                      | Gemini 3.8 Flash TTS | Gemini 3.8 Flash-Lite TTS |
|-------------------------------|----------------------|---------------------------|
| Acehnese (Arab script)        |                      |                           |
| Afrikaans                     |                      |                           |
| Akan                          |                      |                           |
| Amharic                       |                      |                           |
| Armenian                      |                      |                           |
| Assamese                      |                      |                           |
| Awadhi                        |                      |                           |
| Balinese                      |                      |                           |
| Bangla                        |                      |                           |
| Banjar (Arab script)          |                      |                           |
| Banjar (Latn script)          |                      |                           |
| Bashkir                       |                      |                           |
| Basque                        |                      |                           |
| Belarusian                    |                      |                           |
| Bemba                         |                      |                           |
| Bhojpuri                      |                      |                           |
| Bosnian                       |                      |                           |
| Buginese                      |                      |                           |
| Bulgarian                     |                      |                           |
| Burmese                       |                      |                           |
| Cantonese                     |                      |                           |
| Catalan                       |                      |                           |
| Cebuano                       |                      |                           |
| Central Kurdish               |                      |                           |
| Chhattisgarhi                 |                      |                           |
| Chinese (Hans script)         |                      |                           |
| Chinese (Hant script)         |                      |                           |
| Crimean Tatar                 |                      |                           |
| Croatian                      |                      |                           |
| Czech                         |                      |                           |
| Danish                        |                      |                           |
| Dutch                         |                      |                           |
| Dyula                         |                      |                           |
| Dzongkha                      |                      |                           |
| Egyptian Arabic               |                      |                           |
| English                       |                      |                           |
| Estonian                      |                      |                           |
| Filipino                      |                      |                           |
| Finnish                       |                      |                           |
| French                        |                      |                           |
| Galician                      |                      |                           |
| Ganda                         |                      |                           |
| Georgian                      |                      |                           |
| German                        |                      |                           |
| Greek                         |                      |                           |
| Guarani                       |                      |                           |
| Gujarati                      |                      |                           |
| Haitian Creole                |                      |                           |
| Halh Mongolian                |                      |                           |
| Hausa                         |                      |                           |
| Hebrew                        |                      |                           |
| Hindi                         |                      |                           |
| Hungarian                     |                      |                           |
| Icelandic                     |                      |                           |
| Igbo                          |                      |                           |
| Iloko                         |                      |                           |
| Indonesian                    |                      |                           |
| Iranian Persian               |                      |                           |
| Italian                       |                      |                           |
| Japanese                      |                      |                           |
| Javanese                      |                      |                           |
| Kabyle                        |                      |                           |
| Kamba                         |                      |                           |
| Kannada                       |                      |                           |
| Kashmiri (Arab script)        |                      |                           |
| Kashmiri (Deva script)        |                      |                           |
| Kazakh                        |                      |                           |
| Khmer                         |                      |                           |
| Kikuyu                        |                      |                           |
| Kinyarwanda                   |                      |                           |
| Kongo                         |                      |                           |
| Korean                        |                      |                           |
| Kyrgyz                        |                      |                           |
| Lao                           |                      |                           |
| Latgalian                     |                      |                           |
| Lingala                       |                      |                           |
| Lithuanian                    |                      |                           |
| Luxembourgish                 |                      |                           |
| Macedonian                    |                      |                           |
| Magahi                        |                      |                           |
| Maithili                      |                      |                           |
| Malayalam                     |                      |                           |
| Maltese                       |                      |                           |
| Manipuri                      |                      |                           |
| Marathi                       |                      |                           |
| Minangkabau (Arab script)     |                      |                           |
| Minangkabau (Latn script)     |                      |                           |
| Mizo                          |                      |                           |
| Nepali (individual language)  |                      |                           |
| Nigerian Fulfulde             |                      |                           |
| North Azerbaijani             |                      |                           |
| Northern Sotho                |                      |                           |
| Northern Uzbek                |                      |                           |
| Norwegian Bokmål              |                      |                           |
| Norwegian Nynorsk             |                      |                           |
| Nyanja                        |                      |                           |
| Occitan                       |                      |                           |
| Odia (individual language)    |                      |                           |
| Pangasinan                    |                      |                           |
| Persian (Afghanistan)         |                      |                           |
| Polish                        |                      |                           |
| Portuguese                    |                      |                           |
| Punjabi                       |                      |                           |
| Romanian                      |                      |                           |
| Russian                       |                      |                           |
| Santali                       |                      |                           |
| Serbian                       |                      |                           |
| Sindhi                        |                      |                           |
| Sinhala                       |                      |                           |
| Slovak                        |                      |                           |
| Slovenian                     |                      |                           |
| Somali                        |                      |                           |
| South Azerbaijani             |                      |                           |
| Southern Pashto               |                      |                           |
| Southern Sotho                |                      |                           |
| Spanish                       |                      |                           |
| Standard Arabic (Arab script) |                      |                           |
| Standard Arabic (Latn script) |                      |                           |
| Standard Latvian              |                      |                           |
| Standard Malay                |                      |                           |
| Swahili (individual language) |                      |                           |
| Swati                         |                      |                           |
| Swedish                       |                      |                           |
| Tajik                         |                      |                           |
| Tamil                         |                      |                           |
| Telugu                        |                      |                           |
| Thai                          |                      |                           |
| Tigrinya                      |                      |                           |
| Tosk Albanian                 |                      |                           |
| Uyghur                        |                      |                           |

## Limitations

- The TTS models accept text-only input and return audio-only output.
- Multi-speaker requests require exactly two speakers. To combine designed ( `voice_...` ) or replicated ( `voice_...` or `voicekey_...` ) voices in multi-character dialogue, or to use more than two speakers, synthesize each speaker's turn individually and concatenate the audio. Request `AUDIO_L16` output for each turn, or strip the WAV header from each clip before you concatenate the clips.
- The models are available only in the `global` location.
- System instructions aren't supported.
- You can't set the output sample rate. MP3 and Ogg Opus output aren't supported.

## What's next

- Learn how to direct style, pacing, and vocal sounds in the [prompting guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/prompting-guide) .
- Create custom voices from a text description with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) .
- Replicate a speaker's voice with [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .
- Review model specifications on the [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) model pages.
