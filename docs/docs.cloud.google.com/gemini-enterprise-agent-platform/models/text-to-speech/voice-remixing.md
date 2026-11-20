---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-remixing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-remixing
title: Create a custom voice with voice remixing
description: Create a new custom voice by editing an existing voice with a natural-language description, and use it with the Gemini 3.8 TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

> To learn more, run the "Gemini 3.8 Flash TTS" notebook in one of the following environments:
>
> [Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb) \| [Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) \| [Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) \| [View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb)

You can create a new custom voice by editing an existing voice with the *voice remixing* feature. Instead of describing a voice from scratch, you choose a *base voice* and describe the changes to make, such as a different age, pitch, energy, timbre, or accent. The Voices API stores the result as a new voice in your project and returns a reusable `voice_...` ID that you pass in speech generation requests.

You can remix the following voices:

- A [prebuilt voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#prebuilt-voices) , such as `Puck` or `Kore` .
- An [Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library) voice.
- A [designed voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) or a previously remixed voice that's stored in your project.

Remixed voices work with both [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` ) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ).

## How voice remixing works

Voice remixing uses the same Voices API `create` method as [voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) , with the `voice.prompted.base_voice` field added:

1.  **Choose a base voice and describe the changes** : Call the Voices API `create` method with `voice.type` set to `VOICE_TYPE_PROMPTED` , `store` set to `true` , `voice.prompted.base_voice` set to the name or ID of an existing voice, and `voice.prompted.input` set to a description of the changes.
2.  **Receive a new voice ID and a sample** : The Voices API applies your changes to the base voice, stores the result as a new voice in your project, and returns its ID (for example, `voice_abc123...` ) in the `id` field and a sample of the voice in the `sample_audio` field. The base voice doesn't change.
3.  **Generate speech or remix again** : Pass the new voice ID in `speechConfig.voiceConfig.voice` when you call `generateContent` or `streamGenerateContent` . To refine the voice further, pass the new voice ID as the `base_voice` of another `create` request.

## Before you begin

To use the Python samples, install version 2.33.0 or later of the [Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/start/libraries) :

```
pip install --upgrade "google-genai>=2.33.0"
```

The Voices API is available in the `global` location through the `v1beta1` API version.

### Required roles

To get the permissions that you need to remix voices and generate speech with them, ask your administrator to grant you the following IAM roles on your Google Cloud project:

- Create, list, get, and delete voices, and generate speech: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Create a remixed voice

Set the following fields in the request:

- `store` : Must be `true` . Remixed voices are always stored in your project. Requests that set `base_voice` with `store: false` fail with an `INVALID_ARGUMENT` error.
- `voice.type` : `VOICE_TYPE_PROMPTED` .
- `voice.prompted.base_voice` : The voice to remix. Use the voice name for a prebuilt voice (for example, `Puck` ), the voice ID for an Extended Voice Library voice, or the `voice_...` ID for a designed or remixed voice. If the voice doesn't exist, the request fails with a `NOT_FOUND` error.
- `voice.prompted.input` : A natural-language description of the changes to make to the base voice.
- `voice.display_name` , `voice.gender` , `voice.language_code` : Optional metadata for the new voice.

Don't set `voice.model` . Requests that set a model together with `store: true` fail with an `INVALID_ARGUMENT` error.

Remixing a voice can take several seconds. The Python sample sets the request timeout to 60 seconds.

The response contains the following fields:

- `id` : The ID of the new voice.
- `prompted.base_voice` : The base voice that you remixed.
- `sample_audio` : A sample of the new voice. The `data` field holds the base64-encoded audio, and the `mime_type` field names its encoding. By default, the sample is a complete WAV file ( `audio/wav` ) with a RIFF header: 16-bit PCM, 24 kHz, mono. Some voices can return headerless 16-bit PCM ( `audio/l16; rate=24000; channels=1` ) instead, so check `mime_type` before you save the audio.
- `usage` : The number of tokens that the request used. For more information, see [Pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-remixing#pricing) .

The following samples remix the prebuilt `Puck` voice:

### Python

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
import base64
import wave

from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

voice = client.voices.create(
    store=True,
    voice={
        "type": "VOICE_TYPE_PROMPTED",
        "display_name": "Older British Puck",
        "prompted": {
            "base_voice": "Puck",
            "input": (
                "Make the voice sound slightly older and more grounded, with a"
                " warm British accent and measured audiobook narration pacing."
            ),
        },
    },
    timeout=60,
)

print(f"Created voice ID: {voice.id}")

# Save the voice sample. The SDK returns sample_audio.data as a base64
# string. By default, it's a complete WAV file (audio/wav). For
# compatibility, add a WAV header if the sample is raw 16-bit PCM
# (audio/l16).
sample = base64.b64decode(voice.sample_audio.data)
if voice.sample_audio.mime_type.lower().startswith("audio/l16"):
    with wave.open("remixed_voice_sample.wav", "wb") as wf:
        wf.setnchannels(1)
        wf.setsampwidth(2)
        wf.setframerate(24000)
        wf.writeframes(sample)
else:
    with open("remixed_voice_sample.wav", "wb") as f:
        f.write(sample)
```

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices
```

Request JSON body:

```
{
  "store": true,
  "voice": {
    "type": "VOICE_TYPE_PROMPTED",
    "displayName": "Older British Puck",
    "prompted": {
      "baseVoice": "Puck",
      "input": "Make the voice sound slightly older and more grounded, with a warm British accent and measured audiobook narration pacing."
    }
  }
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices" | Select-Object -Expand Content
```

You should receive a JSON response similar to the following. The `sample_audio.data` field is truncated.

```
{
  "id": "voice_7bd85ebf-761b-4969-8544-4ec60f06d124",
  "prompted": {
    "base_voice": "Puck"
  },
  "usage": {
    "total_tokens": 578,
    "total_input_tokens": 297,
    "input_tokens_by_modality": [
      {"modality": "text", "tokens": 38},
      {"modality": "audio", "tokens": 259}
    ],
    "total_output_tokens": 281,
    "output_tokens_by_modality": [
      {"modality": "audio", "tokens": 281}
    ]
  },
  "sample_audio": {
    "mime_type": "audio/wav",
    "data": "UklGRpTwAwBXQVZF..."
  }
}
```

By default, `sample_audio.mime_type` is `audio/wav` , and `sample_audio.data` holds a base64-encoded, complete WAV file. If `mime_type` is `audio/l16` , the decoded data is headerless 16-bit PCM audio at 24 kHz, mono, and needs a WAV header before most players can open it.

## Generate speech with a remixed voice

Pass the voice ID in `speechConfig.voiceConfig.voice` , the same way that you pass a [designed voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design#synthesize) :

### Python

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

response = client.models.generate_content(
    model="gemini-3.8-flash-tts",
    contents=[{
        "role": "user",
        "parts": [{
            "text": "Chapter One. The fog rolled quietly across the harbor at dawn.",
            "speech_metadata": {"style": "calm and reflective"},
        }],
    }],
    config={
        "response_modalities": ["AUDIO"],
        "speech_config": {"voice_config": {"voice": "VOICE_ID"}},
    },
)

# The SDK has already decoded the base64 audio, so inline_data.data is a
# complete WAV file by default.
with open("remixed_voice.wav", "wb") as f:
    f.write(response.candidates[0].content.parts[0].inline_data.data)
```

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` VOICE_ID ` : The voice ID that the Voices API `create` method returned.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent
```

Request JSON body:

```
{
  "contents": [{
    "role": "user",
    "parts": [{
      "text": "Chapter One. The fog rolled quietly across the harbor at dawn.",
      "speechMetadata": {"style": "calm and reflective"}
    }]
  }],
  "generationConfig": {
    "responseModalities": ["AUDIO"],
    "speechConfig": {
      "voiceConfig": {"voice": "VOICE_ID"}
    }
  }
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent" | Select-Object -Expand Content
```

The response contains the audio as a base64-encoded, complete WAV file in `candidates[0].content.parts[0].inlineData.data` . The `data` field is truncated.

```
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "inlineData": {
              "mimeType": "audio/wav",
              "data": "UklGRhRlBABXQVZF..."
            }
          }
        ]
      },
      "finishReason": "STOP"
    }
  ]
}
```

In the Python sample, replace ` PROJECT_ID ` with your Google Cloud project ID and ` VOICE_ID ` with the voice ID that the `create` method returned.

## Refine a voice step by step

Each remixed voice is a stored `voice_...` voice, so you can use it as the base voice of another remix. This step-by-step workflow lets you change one or two traits at a time and listen to each result before you make the next change. You can also start from a designed voice.

The following samples remix an existing designed or remixed voice:

### Python

#### Install

```
pip install --upgrade google-genai
```

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Google Gen AI SDK with Vertex AI:

```
# Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
# with appropriate values for your project.
export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
export GOOGLE_CLOUD_LOCATION=global
export GOOGLE_GENAI_USE_ENTERPRISE=True
```

```
from google import genai

client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")

voice = client.voices.create(
    store=True,
    voice={
        "type": "VOICE_TYPE_PROMPTED",
        "prompted": {
            "base_voice": "BASE_VOICE_ID",
            "input": (
                "Keep the same speaker identity and accent, but make the"
                " delivery calmer, softer, and slightly lower in pitch."
            ),
        },
    },
    timeout=60,
)

print(f"Created voice ID: {voice.id}")
print(f"Remixed from: {voice.prompted.base_voice}")
```

### REST

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` BASE_VOICE_ID ` : The `voice_...` ID of a designed or remixed voice in your project.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices
```

Request JSON body:

```
{
  "store": true,
  "voice": {
    "type": "VOICE_TYPE_PROMPTED",
    "prompted": {
      "baseVoice": "BASE_VOICE_ID",
      "input": "Keep the same speaker identity and accent, but make the delivery calmer, softer, and slightly lower in pitch."
    }
  }
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices" | Select-Object -Expand Content
```

You should receive a JSON response similar to the following. The `sample_audio.data` field is truncated.

```
{
  "id": "voice_f70c942e-7d78-427d-8466-cae3cb9b0371",
  "prompted": {
    "base_voice": "voice_7bd85ebf-761b-4969-8544-4ec60f06d124"
  },
  "sample_audio": {
    "mime_type": "audio/wav",
    "data": "UklGRhT4AgBXQVZF..."
  }
}
```

In the Python sample, replace ` BASE_VOICE_ID ` with the `voice_...` ID of a designed or remixed voice in your project.

## Manage remixed voices

Remixed voices are stored in your project with the type `VOICE_TYPE_PROMPTED` , the same type as designed voices. To list, get, or delete remixed voices, use the same methods as for designed voices. For details, see [Manage stored voices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design#manage) .

A remixed voice is independent of its base voice:

- Remixing never changes the base voice.
- Deleting the base voice doesn't affect voices that were remixed from it.

### Limits

- Stored voices expire one year after they were last used. Generating speech with a voice, or using it as the `base_voice` of a remix, restarts this period. Delete voices that you no longer need.
- Remix requests count toward the same per-project, per-minute voice creation quota as voice design and voice replication. If you exceed it, the `create` method returns a `RESOURCE_EXHAUSTED` error. Wait and retry. For more information, see [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas) .

## Pricing

Remixing a voice is billed at the Gemini 3.8 Flash TTS rates for the following tokens:

- **Text input tokens** for the description in `voice.prompted.input` .
- **Audio input tokens** for the base voice audio.
- **Audio output tokens** for the voice sample that the Voices API generates.

The `usage` field in the `create` response reports each count. For example, the remix in the [create sample](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-remixing#create) uses about 40 text input tokens, about 260 audio input tokens, and about 280 audio output tokens.

The `get` , `list` , and `delete` methods aren't billed. Speech that you generate with a remixed voice is billed at the rates of the model that you call.

For token rates, see [Gemini Enterprise pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Prompting best practices

- **Describe only the changes** : The model keeps the sound of the base voice, so describe only the traits to change, such as age, timbre, pitch, pacing, or energy. Don't repeat the full description of the voice.
- **State a new language or accent explicitly** : A remix keeps the language and regional accent of the base voice unless `voice.prompted.input` asks for a different one.
- **Change one or two traits per step** : When you refine a voice over several remixes, change a small set of traits in each request, and listen to the `sample_audio` before you make the next change.
- **Use remixing for permanent traits and `speech_metadata.style` for each turn** : Use voice remixing to change the baseline of a voice, such as its age, accent, pitch, or persona. Use short `speech_metadata.style` values, such as `"whispered urgently"` or `"excited"` , to direct the delivery of individual turns.

The following table shows example remix requests:

| Goal                   | `base_voice`                     | `prompted.input`                                                                                                          |
|------------------------|----------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Change age and timbre  | `Puck`                           | `Make the voice sound 20 years older with a deeper, slightly gravelly baritone timbre while keeping the friendly warmth.` |
| Change regional accent | `Kore`                           | `Change the accent to Australian English while preserving the clear, confident studio delivery.`                          |
| Adapt to a domain      | A designed voice ( `voice_...` ) | `Adapt this voice for late-night meditation narration: lower the vocal projection, slow the pacing, and soften the tone.` |
| Increase energy        | A remixed voice ( `voice_...` )  | `Increase vocal energy and projection so the speaker sounds like an upbeat live event announcer.`                         |

## What's next

- Create a custom voice from a text description with [voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) .
- Replicate an existing speaker's voice with [voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .
- Learn about turn-level styling, inline tags, and multi-speaker dialogue in [Generate speech with Gemini TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .
