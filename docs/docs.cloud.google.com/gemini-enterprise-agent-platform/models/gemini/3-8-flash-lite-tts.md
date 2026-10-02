---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts
title: Gemini 3.8 Flash-Lite TTS
description: Learn about Gemini 3.8 Flash-Lite TTS, our fast, cost-efficient text-to-speech model for high-throughput production workloads.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini 3.8 Flash-Lite TTS ( `gemini-3.8-flash-lite-tts` ) is Google's fast, cost-efficient text-to-speech model for high-throughput production workloads, available through Gemini Enterprise.

## Capabilities

  - **High-throughput efficiency** : Built for bulk production, conversational voice agent cascades, read-aloud features, and everyday single-speaker speech in 101 languages.
  - **Same schema as Gemini 3.8 Flash TTS** : Uses the same request schema and prompting format as `gemini-3.8-flash-tts` , so you can switch models by changing the model ID.
  - **Voice options** : Works with 30 prebuilt voices, more than 2,000 curated voices in the Extended Voice Library, voices that you create with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) , and voices that you replicate with [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .

For features, code samples, and prompting guidance, see [Generate speech with Gemini TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .

## When to use which TTS model

Both Gemini 3.8 TTS models share the same request schema and prompting format. Choose the model that fits your workload:

| Feature or workload     | Gemini 3.8 Flash-Lite TTS ( `gemini-3.8-flash-lite-tts` )                                                                      | [Gemini 3.8 Flash TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts) ( `gemini-3.8-flash-tts` ) |
| :---------------------- | :----------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| **Primary strength**    | High throughput, low latency, and cost efficiency                                                                              | Voice fidelity, acting nuance, and dialect coverage                                                                                           |
| **Best use cases**      | High-volume production, real-time voice agent cascades, read-aloud features, voice replication, everyday single-speaker speech | Audiobooks, studio narration, complex multi-speaker dialogue, frequent vocal-burst tags, difficult pronunciation, regional dialects           |
| **Supported languages** | 101 languages                                                                                                                  | 130 languages                                                                                                                                 |

[Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

Model ID

`gemini-3.8-flash-lite-tts`

Modalities

description

Text  
Input only

hide\_image

Image  
Not supported

mic

Audio  
Output only

videocam\_off

Video  
Not supported

Token limits

Input token limit

8,192

Output token limit

16,384

Capabilities

  - [Single-speaker speech](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#single-speaker)  
    Supported
  - [Multi-speaker speech](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#multi-speaker)  
    Supported
  - [Streaming](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#streaming)  
    Supported
  - [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design)  
    Supported
  - [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication)  
    Supported

Consumption options

  - [Pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options)  
    Supported

Supported regions

**[Model availability](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations)**

  - Global: `global`

Versions

`gemini-3.8-flash-lite-tts`

  - Launch stage: Preview
  - Release date: September 28, 2026

Supported languages

101 languages. See [Supported languages](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#languages) .

## Get started

The following example generates single-speaker speech and saves it as a WAV file:

### Python

    from google import genai
    
    client = genai.Client(enterprise=True, project="PROJECT_ID", location="global")
    
    response = client.models.generate_content(
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
    
    # The SDK has already decoded the base64 audio, so inline_data.data is a
    # complete WAV file by default.
    with open("out.wav", "wb") as f:
        f.write(response.candidates[0].content.parts[0].inline_data.data)

### REST

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth print-access-token)" \
      -H "Content-Type: application/json" \
      https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-3.8-flash-lite-tts:generateContent \
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

If you use `gemini-3.1-flash-tts-preview` or another earlier Gemini TTS model, see the [migration guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide) .
