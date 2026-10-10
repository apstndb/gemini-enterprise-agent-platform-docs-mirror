---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-8-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-8-live
title: Developer&#39;s guide to Gemini 3.8 Live
description: Developer guide for Gemini 3.8 Live, covering real-time bidirectional audio and video streaming, Live Avatar synthesis, asynchronous function calling, and migration from Gemini 2.5 Flash Live API Native Audio.
data_source: docs.cloud.google.com
---

**Gemini 3.8 Live** is a real-time conversational model built for low-latency bidirectional voice and video interactions and face-to-face Live Avatar synthesis. Designed for continuous conversational workflows, 3.8 Live provides default-enabled affective dialogue, proactive audio filtering, auto-canceling blocking tools, and dynamic multilingual switching.

This document covers the following topics:

- How 3.8 Live fits in the Gemini model family.
- Key capabilities in 3.8 Live.
- Integration with the Google Gen AI SDK.
- Required API rules and conventions.
- Migration from earlier Gemini Live API models.

## Role in the Gemini family

3.8 Live is designed for **real-time streaming interactions** . It operates across bidirectional WebSockets, processing speech, live camera feeds, and screen broadcasts with sub-second latency while generating 24 kHz audio and synchronized 24 FPS video avatars.

### Model specifications and comparisons

The following table compares specifications between 3.8 Live and earlier Gemini Live API models:

| Attribute                      | Gemini 3.8 Live                                                                 | Gemini 2.5 Flash Live API Native Audio (GA baseline) |
|--------------------------------|---------------------------------------------------------------------------------|------------------------------------------------------|
| **Model ID**                   | `gemini-3.8-live`                                                               | `gemini-live-2.5-flash-native-audio`                 |
| **Launch stage**               | General Availability (GA)                                                       | General Availability (GA)                            |
| **Input modalities**           | Audio (16 kHz PCM), video (1 FPS JPEG), text                                    | Audio (16 kHz PCM), video (1 FPS JPEG), text         |
| **Output modalities**          | Audio (24 kHz PCM), video (24 FPS MP4 Live Avatar), text                        | Audio (24 kHz PCM), text                             |
| **Live Avatar synthesis**      | 24 FPS synchronized video output                                                | Unsupported                                          |
| **Affective dialogue**         | Enabled by default                                                              | Requires explicit configuration                      |
| **Proactive audio**            | Enabled by default                                                              | Requires explicit configuration                      |
| **Function calling execution** | Asynchronous non-blocking and auto-canceling blocking ( `behavior="BLOCKING"` ) | Asynchronous and synchronous                         |
| **Barge-in handling**          | Polite interruption downgrade (waits when user speaks)                          | Immediate interruption (can overlap user audio)      |
| **Language support**           | Dynamic mid-stream switching across supported languages                         | Supported languages                                  |
| **Domain biasing**             | Supports `custom_vocabulary` in `AudioTranscriptionConfig`                      | Standard baseline transcription                      |
| **Visual token control**       | Configurable `media_resolution` ( `LOW` , `MEDIUM` , `HIGH` )                   | Fixed per-frame token budget                         |

### When to use Gemini 3.8 Live

Use 3.8 Live in the following scenarios:

- You need low conversational latency, natural turn-taking, and fast recovery when the user interrupts (barge-in).
- Your app calls external tools and needs non-blocking execution so audio output continues while backend systems process requests.
- You want to render talking digital avatars with synchronized facial animation and lip-syncing at 24 FPS without external rendering pipelines.
- Your users converse across multiple languages, requiring mid-stream language detection and switching across supported languages.
- You need domain-specific vocabulary biasing for technical terminology, SKUs, or brand names.

For full specifications and quota limits, see the [3.8 Live model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live) .

## Key capabilities in Gemini 3.8 Live

3.8 Live introduces the following capabilities:

- **24 FPS Live Avatar video synthesis** : 3.8 Live generates synchronized 24 FPS MP4 video streams ( `response_modalities=["VIDEO"]` ) directly from model output. Generated facial expressions and lip movements align with synthesized speech in real time.

  You can use prebuilt stock avatars or provide custom reference images to build digital concierges, customer service agents, virtual tutors, or interactive characters. For setup details, see [Configure live avatars](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars) .

- **Default-enabled affective dialogue and proactive audio** :

  - **Affective dialogue** : Enabled by default in 3.8 Live. The model processes acoustic prosody, vocal cues, pauses, and speech inflection in user audio input to adjust vocal tone and conversational pacing.
  - **Proactive audio** : Enabled by default in 3.8 Live. The model filters ambient noise and background speech, generating audio responses only when addressed by the user.

- **Asynchronous and auto-canceling blocking function calling** : 3.8 Live provides tool-calling behaviors designed for real-time speech:

  - **Non-blocking asynchronous execution** : When the model generates a tool call, the audio session stays active so the agent can stream conversational acknowledgments ( *"Let me pull up your account details..."* ) and handle follow-up input while your client app calls backend APIs.
  - **Auto-canceling blocking calls ( `behavior="BLOCKING"` )** : When a function declaration sets `behavior="BLOCKING"` , generation pauses until the tool response arrives. If new user input arrives while the blocking call runs, the Gemini Live API server cancels the pending call.
  - **Polite interruption handling** : In earlier models, returning a tool response with `scheduling="INTERRUPT"` while the user spoke overlapped user audio. In 3.8 Live, the server downgrades the schedule to `WHEN_IDLE` when user speech is active and plays the response after the user finishes speaking.

- **Dynamic multilingual switching and custom vocabulary** :

  - **Multilingual support** : Detects and switches between supported languages mid-session without restarting or reconfiguring the connection.
  - **Custom vocabulary biasing** : Accepts domain-specific keywords, proper nouns, medical terms, and product codes in `AudioTranscriptionConfig` (through `input_audio_transcription` ) using `custom_vocabulary` to improve transcription accuracy.

- **Multimodal visual grounding with `media_resolution` control** : Accepts real-time video streams (1 FPS JPEG frames, recommended resolution `768x768` ) and lets you configure `media_resolution` ( `MEDIA_RESOLUTION_LOW` , `MEDIA_RESOLUTION_MEDIUM` , `MEDIA_RESOLUTION_HIGH` ) to balance per-frame token usage and visual detail.

## Quickstart

Before you begin, authenticate to Google Cloud using Application Default Credentials (ADC).

In the following code sample, replace `PROJECT_ID` with your Google Cloud project ID.

### Install the SDK

Install or update the Google Gen AI SDK and audio dependencies:

```
pip install --upgrade google-genai websockets numpy
```

### Start a bidirectional session with asynchronous tool calling

The following example establishes a real-time session with `gemini-3.8-live` , configures custom vocabulary biasing, and runs non-blocking asynchronous function calls:

```
import asyncio
from google import genai
from google.genai import types

PROJECT_ID = "PROJECT_ID"
LOCATION = "us-central1"
MODEL_ID = "gemini-3.8-live"

# Initialize the Gen AI client for enterprise.
client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

# Define a tool for asynchronous execution.
order_lookup_tool = types.FunctionDeclaration(
    name="lookup_order_status",
    description="Fetches real-time shipping status for a customer order ID.",
    parameters=types.Schema(
        type="OBJECT",
        properties={
            "order_id": types.Schema(
                type="STRING",
                description="The order ID, for example, ORD-8472",
            ),
        },
        required=["order_id"],
    ),
)

# Configure the live connection.
config = types.LiveConnectConfig(
    response_modalities=["AUDIO"],
    system_instruction=types.Content(
        parts=[
            types.Part.from_text(
                text=(
                    "You are an enterprise concierge. When you call a tool, "
                    "briefly acknowledge the request and tell the user what you're doing. "
                    "If a tool returns no results, inform the user before trying again. "
                    "Never issue more than two consecutive tool calls without speaking."
                )
            )
        ]
    ),
    speech_config=types.SpeechConfig(
        voice_config=types.VoiceConfig(
            prebuilt_voice_config=types.PrebuiltVoiceConfig(voice_name="Aoede")
        ),
    ),
    input_audio_transcription=types.AudioTranscriptionConfig(
        custom_vocabulary=["ORD-8472", "Gemini Live", "Express Shipping"]
    ),
    output_audio_transcription=types.AudioTranscriptionConfig(),
    tools=[types.Tool(function_declarations=[order_lookup_tool])],
)

async def handle_tool_call(session, function_call):
    """Executes backend calls asynchronously without blocking incoming audio."""
    order_id = function_call.args.get("order_id", "")
    await asyncio.sleep(2.0)  # Simulate backend API latency.

    if not order_id.startswith("ORD-"):
        result = {
            "status": "invalid_argument",
            "retryable": False,
            "message": f"Order ID '{order_id}' is invalid. Ask the user to verify.",
        }
    else:
        result = {
            "status": "ok",
            "retryable": False,
            "order_id": order_id,
            "shipping_status": "Out for delivery by 4:00 PM",
        }

    # Send tool response matching the call ID.
    await session.send_tool_response(
        function_responses=[
            types.FunctionResponse(
                id=function_call.id,
                name=function_call.name,
                response=result,
            )
        ]
    )

async def main():
    async with client.aio.live.connect(model=MODEL_ID, config=config) as session:
        print(f"Connected to {MODEL_ID}")

        # Send initial text or stream 16 kHz PCM audio chunks.
        await session.send_realtime_input(
            text="Hi! Can you check the status of order ORD-8472?"
        )

        async for message in session.receive():
            # Handle asynchronous tool calls.
            if message.tool_call:
                for call in message.tool_call.function_calls:
                    asyncio.create_task(handle_tool_call(session, call))

            # Process audio output chunks and transcriptions.
            if message.server_content:
                if (
                    message.server_content.output_transcription
                    and message.server_content.output_transcription.text
                ):
                    print(
                        f"Agent: {message.server_content.output_transcription.text}",
                        end="",
                        flush=True,
                    )

if __name__ == "__main__":
    asyncio.run(main())
```

## Required API rules and conventions

When building with 3.8 Live, follow these API conventions:

- **Informative function responses** : Don't return an empty dictionary ( `{}` ) or `None` from a tool handler. When a tool returns an error or empty payload, 3.8 Live might generate repeat function calls with modified arguments unless the response includes status fields. Return structured fields in every tool response:
  - `status` : A machine-readable status string, such as `"ok"` , `"no_results"` , or `"invalid_argument"` .
  - `retryable` : Set to `false` when repeating the call returns the same result.
  - `message` or `guidance` : Text specifying the status to report to the user.
- **Prompt-level tool retry limits** : Include a retry limit in your `system_instruction` . For example: *"If a tool call returns no results, inform the user instead of searching repeatedly with parameter variations. Never run more than two consecutive tool calls without speaking to the user."*
- **Strict `FunctionResponse` matching** :
  - Every `FunctionResponse` turn must supply the exact `id` from the preceding `FunctionCall` .
  - Pass response objects directly in `FunctionResponse.response` .
- **Streaming audio formats** :
  - Input audio: 16 kHz, 16-bit, little-endian, mono PCM ( `audio/pcm;rate=16000` ), streamed in chunks of 20 ms to 100 ms.
  - Output audio: 24 kHz mono PCM.
- **Removed legacy parameters** : Don't pass `enable_affective_dialog` or `proactivity` in your configuration; these features are enabled by default in 3.8 Live.
- **Seeding conversation history** : If you seed multi-turn history using `send_client_content` , wait until the client app receives the `setup_complete` server frame and configure `HistoryConfig(initial_history_in_client_content=True)` .

## Migrate to Gemini 3.8 Live

For more information about migrating from `gemini-live-2.5-flash-native-audio` to `gemini-3.8-live` , see [Migrate from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/migrate-from-gemini-2-5-to-gemini-3-8-live) .

## Developer checklist

Verify the following items before deploying your app:

Target model ID: `gemini-3.8-live`

Return structured tool responses containing `status` , `retryable` , and `message` fields.

Include an explicit retry policy in `system_instruction` capping consecutive tool calls at two.

Remove legacy `enable_affective_dialog` and `proactivity` configuration fields.

Verify audio streams: 16 kHz mono PCM input and 24 kHz output.

Add domain-specific keywords and SKUs using `custom_vocabulary` in `AudioTranscriptionConfig` .

## Additional resources

For more information, see the following resources:

- [Gemini 3.8 Live model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live)
- [Configure live avatars](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars)
- [Best practices with Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/best-practices)
- [Migrate from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/migrate-from-gemini-2-5-to-gemini-3-8-live)
- [Multimodal Live API Python tutorial](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api.ipynb)
- [Intro to Live Avatar notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_live_avatar.ipynb)
- [Gemini Live API Service Skill](https://github.com/google/skills/blob/main/skills/cloud/gemini-live-api/SKILL.md)
