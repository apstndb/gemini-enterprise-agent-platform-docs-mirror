---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-tts
title: Gemini 3.8 Flash TTS
description: Learn about Gemini 3.8 Flash TTS, our text-to-speech model for studio-grade voice fidelity, expressive acting, regional accents, and stable long-form multi-speaker audio.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is a Generative AI Preview offering, subject to the "Pre-GA Offerings Terms" of the [Google Cloud Service Specific Terms](https://cloud.google.com/terms/service-terms) . For this Generative AI Preview offering, Customers may elect to use it for production or commercial purposes, or disclose Generated Output to third-parties, and may process personal data as outlined in the [Cloud Data Processing Addendum](https://cloud.google.com/terms/data-processing-addendum) , subject to the obligations and restrictions described in the agreement under which you access Google Cloud.

Gemini 3.8 Flash TTS ( `gemini-3.8-flash-tts` ) is Google's flagship text-to-speech model, available through Gemini Enterprise. It's built for studio-grade voice fidelity, expressive acting, authentic regional accents, and stable long-form, multi-turn audio.

## Capabilities

- **Acoustic fidelity and acting nuance** : Delivers a wide emotional range, natural cadence, and close adherence to turn-level `style` directions and inline vocal events such as `<laugh>` , `<sigh>` , and `<short pause>` .
- **Long-form, multi-turn stability** : Keeps voice identity, timbre, volume, and room tone consistent across long dialogues and multi-minute narration.
- **Regional accents and pronunciation** : Supports regional accents and minority dialects in 130 languages.
- **Voice options** : Works with 30 prebuilt voices, more than 2,000 curated voices in the Extended Voice Library, voices that you create with [Voice design](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design) , and voices that you replicate with [Voice replication](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication) .

For features, code samples, and prompting guidance, see [Generate speech with Gemini TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview) .

## When to use which TTS model

Both Gemini 3.8 TTS models share the same request schema and prompting format. Choose the model that fits your workload:

| Feature or workload     | Gemini 3.8 Flash TTS ( `gemini-3.8-flash-tts` )                                                                                     | [Gemini 3.8 Flash-Lite TTS](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash-lite-tts) ( `gemini-3.8-flash-lite-tts` ) |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Primary strength**    | Voice fidelity, acting nuance, and dialect coverage                                                                                 | High throughput, low latency, and cost efficiency                                                                                                            |
| **Best use cases**      | Audiobooks, studio narration, complex multi-speaker dialogue, frequent vocal-burst tags, difficult pronunciation, regional dialects | High-volume production, real-time voice agent cascades, read-aloud features, voice replication, everyday single-speaker speech                               |
| **Supported languages** | 130 languages                                                                                                                       | 101 languages                                                                                                                                                |

[Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th>Model ID</th>
<th><code>gemini-3.8-flash-tts</code></th>
<td></td>
</tr>
<tr class="even">
<th>Modalities</th>
<th>description
Text<br />
Input only
hide_image
Image<br />
Not supported
mic
Audio<br />
Output only
videocam_off
Video<br />
Not supported</th>
<td></td>
</tr>
<tr class="odd">
<th>Token limits</th>
<th>Input token limit</th>
<td>8,192</td>
</tr>
<tr class="even">
<th>Output token limit</th>
<th>16,384</th>
<td></td>
</tr>
<tr class="odd">
<th>Capabilities</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#single-speaker">Single-speaker speech</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#multi-speaker">Multi-speaker speech</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#streaming">Streaming</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-design">Voice design</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/voice-replication">Voice replication</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>APIs</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/inference">GenerateContent API</a><br />
Supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions">Interactions API</a> preview Preview feature<br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api">Gemini Live API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/get-token-count">Count Tokens API</a><br />
Not supported</li>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/overview">Chat Completions API</a><br />
Not supported</li>
</ul></th>
<td></td>
</tr>
<tr class="odd">
<th>Consumption options</th>
<th><ul>
<li><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options">Pay-as-you-go</a><br />
Supported</li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported regions</th>
<th><p><strong><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations">Model availability</a></strong></p></th>
<td><ul>
<li>Global: <code>global</code></li>
</ul></td>
</tr>
<tr class="odd">
<th>Versions</th>
<th><ul>
<li><code>gemini-3.8-flash-tts</code>
<ul>
<li>Launch stage: Preview</li>
<li>Release date: September 28, 2026</li>
</ul></li>
</ul></th>
<td></td>
</tr>
<tr class="even">
<th>Supported languages</th>
<th>130 languages. See <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/overview#languages">Supported languages</a> .</th>
<td></td>
</tr>
</tbody>
</table>

## Get started

The following example generates single-speaker speech and saves it as a WAV file:

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

If you use an earlier Gemini TTS model, see the [migration guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/text-to-speech/migration-guide) .
