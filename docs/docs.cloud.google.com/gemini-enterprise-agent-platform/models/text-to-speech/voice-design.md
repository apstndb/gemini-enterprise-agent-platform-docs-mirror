---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design
title: Create a custom voice with voice design
description: Learn how to create a custom voice from a natural-language description and use it with the Gemini 3.8 TTS models on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

> To learn more, run the "Gemini 3.8 Flash TTS" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Faudio%2Fspeech%2Fgetting-started%2Fgemini_3_8_flash_tts.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/audio/speech/getting-started/gemini_3_8_flash_tts.ipynb)

You can create a custom voice from a natural-language description using the *voice design* feature. Instead of choosing a prebuilt voice or recording reference audio, you create a voice by describing a character's age, vocal timbre, accent, and baseline delivery. The Voices API stores the voice in your project and returns a reusable `voice_...` ID that you pass in speech generation requests.

Designed voices work with both [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` ) and [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ).

## How voice design works

1.  **Create a prompted voice** : Call the Voices API `create` method with `voice.type` set to `VOICE_TYPE_PROMPTED` and `store` set to `true` .
2.  **Receive a voice ID and a sample** : The Voices API generates the voice, stores it in your project, and returns its ID (for example, `voice_abc123...` ) in the `id` field and a sample of the voice in the `sample_audio` field.
3.  **Generate speech** : Pass the voice ID in `speechConfig.voiceConfig.voice` when you call `generateContent` or `streamGenerateContent` .

## Before you begin

Complete the steps in [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#before-you-begin) on the Gemini TTS page. The Voices API is available in the `global` location through the `v1beta1` API version.

## Create a designed voice

Set the following fields in the request:

  - `store` : Must be `true` . Designed voices are always stored in your project.
  - `voice.type` : `VOICE_TYPE_PROMPTED` .
  - `voice.prompted.input` : A natural-language description of the voice.
  - `voice.display_name` , `voice.gender` , `voice.language_code` : Optional metadata for the voice.

Don't set `voice.model` . Requests that set a model together with `store: true` fail with an `INVALID_ARGUMENT` error.

Designing a voice can take several seconds. The Python sample sets the request timeout to 60 seconds.

The response contains the following fields:

  - `id` : The ID of the new voice.

  - `sample_audio` : A sample of the voice. The `data` field holds the base64-encoded audio, and the `mime_type` field names its encoding. For example, `audio/l16; rate=24000; channels=1` is headerless 16-bit PCM at 24 kHz, mono.

  - `usage` : The number of tokens that the request used. For more information, see [Pricing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design#pricing) .

### Python

    import base64
    import wave
    
    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    voice = client.voices.create(
        store=True,
        voice={
            "type": "VOICE_TYPE_PROMPTED",
            "display_name": "Warm British Astronomer",
            "gender": "male",
            "language_code": "en-GB",
            "prompted": {
                "input": (
                    "A warm, thoughtful astronomer in his late 60s with a gentle"
                    " British accent, speaking with quiet wonder."
                )
            },
        },
        timeout=60,
    )
    
    print(f"Created voice ID: {voice.id}")
    
    # Save the voice sample. The SDK returns sample_audio.data as a base64
    # string. Raw 16-bit PCM (audio/l16) needs a WAV header.
    sample = base64.b64decode(voice.sample_audio.data)
    if voice.sample_audio.mime_type.lower().startswith("audio/l16"):
        with wave.open("voice_sample.wav", "wb") as wf:
            wf.setnchannels(1)
            wf.setsampwidth(2)
            wf.setframerate(24000)
            wf.writeframes(sample)
    else:
        with open("voice_sample.wav", "wb") as f:
            f.write(sample)

### REST

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices \
      -d '{
        "store": true,
        "voice": {
          "type": "VOICE_TYPE_PROMPTED",
          "displayName": "Warm British Astronomer",
          "gender": "male",
          "languageCode": "en-GB",
          "prompted": {
            "input": "A warm, thoughtful astronomer in his late 60s with a gentle British accent, speaking with quiet wonder."
          }
        }
      }' > created_voice.json
    
    # Print the voice ID and the encoding of the voice sample.
    jq -r '.id, .sample_audio.mime_type' created_voice.json
    
    # Decode the voice sample.
    jq -r '.sample_audio.data' created_voice.json | base64 --decode > voice_sample.pcm

If `sample_audio.mime_type` is `audio/l16` , the `voice_sample.pcm` file contains headerless 16-bit PCM audio at 24 kHz, mono.

To hear the voice with your own text, generate speech with it as shown in the next section.

## Generate speech with a designed voice

Pass the voice ID in `speechConfig.voiceConfig.voice` :

### Python

    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    response = client.models.generate_content(
        model="gemini-3.8-flash-tts",
        contents=[{
            "role": "user",
            "parts": [{
                "text": (
                    "Look out past the rings of Saturn. Those faint photons left"
                    " their source millions of years ago."
                ),
                "speech_metadata": {"style": "reflective and awe-inspired"},
            }],
        }],
        config={
            "response_modalities": ["AUDIO"],
            "speech_config": {"voice_config": {"voice": "VOICE_ID"}},
        },
    )
    
    # The SDK has already decoded the base64 audio, so inline_data.data is a
    # complete WAV file by default.
    with open("designed_voice.wav", "wb") as f:
        f.write(response.candidates[0].content.parts[0].inline_data.data)

### REST

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-tts:generateContent \
      -d '{
        "contents": [{
          "role": "user",
          "parts": [{
            "text": "Look out past the rings of Saturn. Those faint photons left their source millions of years ago.",
            "speechMetadata": {"style": "reflective and awe-inspired"}
          }]
        }],
        "generationConfig": {
          "responseModalities": ["AUDIO"],
          "speechConfig": {
            "voiceConfig": {"voice": "VOICE_ID"}
          }
        }
      }' | jq -r '.candidates[0].content.parts[0].inlineData.data' | base64 --decode > designed_voice.wav

Replace VOICE\_ID with the voice ID that the `create` method returned.

## Manage stored voices

You can list, get, and delete the voices stored in your project, including designed voices and [stored replicated voices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication#create-stored) . The `list` method returns the voices stored in your project, followed by the prebuilt and [Extended Voice Library](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#voice-library) voices. To list only the voices stored in your project, set the `type` filter to `prompted` and `replicated` , as the following samples do. The `get` method also returns the sample of a designed voice in the `sample_audio` field.

### Python

    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    # List the voices stored in your project.
    for voice in client.voices.list(type_=["prompted", "replicated"]).voices or []:
        print(voice.id, voice.display_name, voice.type)
    
    # Get a voice by ID.
    voice = client.voices.get(id="VOICE_ID")
    
    # Delete a voice.
    client.voices.delete(id="VOICE_ID")

### REST

    # List the voices stored in your project.
    curl -G \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices \
      --data-urlencode "type=prompted" \
      --data-urlencode "type=replicated"
    
    # Get a voice by ID.
    curl -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices/VOICE_ID
    
    # Delete a voice.
    curl -X DELETE \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/voices/VOICE_ID

### Limits

  - Stored voices expire one year after they were last used. Generating speech with a voice restarts this period, so a voice that you use regularly doesn't expire. Delete voices that you no longer need.
  - Voice creation requests are subject to a per-project, per-minute quota. If you exceed it, the `create` method returns a `RESOURCE_EXHAUSTED` error. Wait and retry. For more information, see [Quotas and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas) .

## Pricing

Creating a designed voice is billed as text input tokens and audio output tokens at the Gemini 3.8 Flash TTS rates. The audio output tokens cover the voice sample that the Voices API generates. The `usage` field in the `create` response reports both counts. For example, the one-sentence description in the [create sample](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design#create) uses about 220 input tokens and about 1,100 output tokens.

The `get` , `list` , and `delete` methods aren't billed. Speech that you generate with a designed voice is billed at the rates of the model that you call.

For token rates, see [Gemini Enterprise pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

## Prompting best practices

  - **Put permanent traits in the voice description** : Define age, gender, timbre, vocal texture, and regional accent when you create the voice, not in `speech_metadata.style` .
  - **Use `speech_metadata.style` for situational emotion** : After you create the voice, use short `style` values, such as `"whispered urgently"` or `"cheerful and energetic"` , to direct each turn without changing the speaker's identity.
  - **Be specific and concise** : A clear one- or two-sentence description, such as *"A crisp, energetic sports announcer in her 30s with a slight Midwestern accent"* , produces more consistent results than a long or contradictory paragraph.

## What's next

  - Replicate an existing speaker's voice with [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .
  - Learn about turn-level styling, inline tags, and multi-speaker dialogue in [Generate speech with Gemini TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .
