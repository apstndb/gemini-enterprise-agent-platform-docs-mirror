---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-8-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/gemini-3-8-live
title: Developer&#39;s guide to Gemini 3.8 Live
description: Developer guide for Gemini 3.8 Live, covering real-time bidirectional audio and video streaming, Live Avatar synthesis, asynchronous function calling, and migration from Gemini 2.5 Flash Live API Native Audio.
data_source: docs.cloud.google.com
---

**Gemini 3.8 Live** is our real-time conversational model, engineered for ultra-low latency, bidirectional voice and video interactions, and face-to-face Live Avatar synthesis. Built for continuous conversational experiences, 3.8 Live brings always-on affective dialogue, proactive audio filtering, auto-canceling blocking tools, and dynamic multilingual switching.

This guide covers how the following:

  - How 3.8 Live fits within the Gemini model family.
  - What's new in this release.
  - How to integrate the model using the Google Gen AI SDK.
  - Mandatory API rules.
  - How to migrate from legacy Gemini Live API models.

## How does it fit in the Gemini family?

3.8 Live is built specifically for **real-time streaming interactions** . It operates across bidirectional WebSockets, processing speech, live camera feeds, and screen broadcasts with sub-second latency while synthesizing natural 24 kHz audio and synchronized 24 FPS video avatars.

### Model specifications and comparisons

The following table compares specifications between 3.8 Live and earlier Gemini Live API generations:

| Attribute                      | Gemini 3.8 Live                                                                 | Gemini 2.5 Flash Live API Native Audio (GA baseline) |
| ------------------------------ | ------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **Model ID**                   | `gemini-3.8-live`                                                               | `gemini-live-2.5-flash-native-audio`                 |
| **Launch stage**               | General Availability (GA)                                                       | General Availability (GA)                            |
| **Input modalities**           | Audio (16 kHz PCM), video (1 FPS JPEG), text                                    | Audio (16 kHz PCM), video (1 FPS JPEG), text         |
| **Output modalities**          | Audio (24 kHz PCM), video (24 FPS MP4 Live Avatar), text                        | Audio (24 kHz PCM), text                             |
| **Live Avatar synthesis**      | 24 FPS synchronized video output                                                | Unsupported                                          |
| **Affective dialogue**         | Enabled by default                                                              | Requires explicit configuration                      |
| **Proactive audio**            | Enabled by default                                                              | Requires explicit configuration                      |
| **Function calling execution** | Asynchronous non-blocking and auto-canceling blocking ( `behavior="BLOCKING"` ) | Asynchronous and synchronous                         |
| **Barge-in handling**          | Polite interruption downgrade (waits if user is speaking)                       | Immediate interruption (can talk over user)          |
| **Language support**           | Dynamic mid-stream switching across supported languages                         | Supported languages                                  |
| **Domain biasing**             | Supports `custom_vocabulary` in `AudioTranscriptionConfig`                      | Standard baseline transcription                      |
| **Visual token control**       | Configurable `media_resolution` ( `LOW` , `MEDIUM` , `HIGH` )                   | Fixed per-frame token budget                         |

### When to choose Gemini 3.8 Live

  - **Choose 3.8 Live when** :
      - You need ultra-low conversational latency, natural turn-taking, and instant recovery when the user interrupts (barge-in).
      - Your application calls external tools and needs non-blocking execution so the agent continues speaking while backend systems process requests.
      - You want to render talking digital avatars with synchronized facial animation and lip-syncing at 24 FPS without external rendering pipelines.
      - Your users converse across multiple languages, requiring mid-stream language detection and switching across supported languages.
      - You need domain-specific vocabulary biasing for technical terminology, SKUs, or brand names.

See the [3.8 Live model page](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live) for full specifications and quota limits.

## What's new in Gemini 3.8 Live?

  - 24 FPS Live Avatar video synthesis
    
    3.8 Live can generate synchronized, 24 FPS MP4 video streams ( `response_modalities=["VIDEO"]` ) directly from the model. The generated avatar's facial expressions and lip movements sync with the synthesized speech in real time.
    
    You can use either prebuilt stock avatars or provide custom reference images to build engaging digital concierges, customer service representatives, virtual tutors, or interactive game characters. For setup details, see [Configure live avatars](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars) .

  - Always-on affective dialogue and proactive audio
    
      - **Affective dialogue** : Enabled by default in 3.8 Live. The model listens to acoustic prosody, emotional cues, pauses, and speech inflection in the user's audio input, adjusting its vocal tone, empathy, and conversational rhythm naturally.
    
      - **Proactive audio** : Enabled by default in 3.8 Live. The model automatically filters out ambient noise and off-topic background chatter, responding only when addressed directly by the user.

  - Asynchronous and auto-canceling blocking function calling
    
    3.8 Live introduces robust tool calling mechanics designed for real-time speech:
    
      - **Non-blocking asynchronous execution** : When the model initiates a tool call, the audio session doesn't freeze. The agent can provide natural conversational fillers ( *"Let me pull up your account details..."* ) and answer follow-up questions while your client executes backend APIs.
    
      - **Auto-canceling blocking calls ( `behavior="BLOCKING"` )** : When a function declaration specifies `behavior="BLOCKING"` , the model pauses for the tool response. If the user speaks again while the tool call is in flight, the Gemini Live API server automatically cancels the pending call so the agent can pivot immediately to the user's newest request.
    
      - **Polite interruption handling** : In earlier models, returning a tool response with `scheduling="INTERRUPT"` while the user was speaking caused the agent to talk over the user. In 3.8 Live, the server automatically downgrades the schedule to `WHEN_IDLE` if the user is speaking, playing the tool response only after the user pauses.

  - Dynamic multilingual switching and custom vocabulary
    
      - **Multilingual support** : Automatically detects and transitions between supported languages mid-conversation without needing session restarts or manual reconfiguration.
      - **Custom vocabulary biasing** : You can pass domain-specific keywords, proper nouns, medical terms, and product codes into `AudioTranscriptionConfig` (via `input_audio_transcription` ) using `custom_vocabulary` , significantly improving recognition accuracy for specialized terms.

  - Multimodal visual grounding with `media_resolution` control
    
    3.8 Live ingests real-time video feeds (1 FPS JPEG frames, optimal resolution `768x768` ) and lets you set `media_resolution` ( `MEDIA_RESOLUTION_LOW` , `MEDIA_RESOLUTION_MEDIUM` , `MEDIA_RESOLUTION_HIGH` ) to balance per-frame token consumption against fine visual detail.

## Quickstart

Before you begin, ensure you have authenticated to Google Cloud with Application Default Credentials (ADC).

In the following code sample, replace PROJECT\_ID with your Google Cloud project ID.

### Installation

Install or upgrade the latest Google Gen AI SDK and audio utilities:

    pip install --upgrade google-genai websockets numpy

### Bidirectional session with asynchronous tool calling

The following example establishes a real-time session with `gemini-3.8-live` , sets up custom vocabulary biasing, and demonstrates non-blocking asynchronous function execution:

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

## Mandatory API rules and behavioral conventions

When building with 3.8 Live, you must follow these API conventions:

  - **Informative function responses** : Never return an empty dictionary ( `{}` ) or bare `None` from a tool handler. When a tool fails or finds no results, 3.8 Live attempts to re-query with variations unless explicitly told not to. Always return structured metadata:
      - `status` : A machine-readable status string (such as `"ok"` , `"no_results"` , or `"invalid_argument"` ).
      - `retryable` : Set to `false` when retrying won't change the outcome.
      - `message` or `guidance` : A clear explanation advising the model what to say to the user.
  - **Prompt-level tool retry limits** : Always include a retry constraint in your `system_instruction` . For example: *"If a tool call returns no results, inform the user instead of searching repeatedly with parameter variations. Never run more than two consecutive tool calls without speaking to the user."*
  - **Strict `FunctionResponse` matching** :
      - Every `FunctionResponse` turn must supply the exact `id` from the preceding `FunctionCall` .
      - Pass response objects directly in `FunctionResponse.response` .
  - **Streaming audio formats** :
      - Input audio: 16 kHz, 16-bit, little-endian, mono PCM ( `audio/pcm;rate=16000` ), streamed in chunks of 20 ms to 100 ms.
      - Output audio: 24 kHz mono PCM.
  - **Removed legacy flags** : Do not pass `enable_affective_dialog` or `proactivity` in your configuration. These features are enabled by default in 3.8 Live.
  - **Seeding conversation history** : If you seed multi-turn history using `send_client_content` , wait until the client receives the `setup_complete` server frame and configure `HistoryConfig(initial_history_in_client_content=True)` .

## Migrate to Gemini 3.8 Live

For information about migrating from gemini-live-2.5-flash-native-audio to gemini-3.8-live, see [Migrate from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/migrate-from-gemini-2-5-to-gemini-3-8-live) .

## Summary checklist for developers

Target model ID: `gemini-3.8-live`

Return structured, informative tool responses containing `status` , `retryable` , and `message` fields.

Include an explicit retry policy in `system_instruction` capping consecutive tool calls at two.

Remove deprecated `enable_affective_dialog` and `proactivity` flags.

Verify audio streams: 16 kHz mono PCM input and 24 kHz output.

Add domain-specific keywords and SKUs using `custom_vocabulary` in `AudioTranscriptionConfig` .

## Additional resources

  - [Gemini 3.8 Live model reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live)

  - [Gemini Live API prompt guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/live-api-prompt-guide)

  - [Configure live avatars](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars)

  - [Best practices with Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/best-practices)

  - [Migrate from Gemini 2.5 Flash Live API Native Audio to Gemini 3.8 Live](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/guides/migrate-from-gemini-2-5-to-gemini-3-8-live)

  - [Multimodal Live API Python tutorial](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api.ipynb)

  - [Intro to Live Avatar notebook](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_live_avatar.ipynb)

  - [Gemini Live API Service Skill](https://github.com/google/skills/blob/main/skills/cloud/gemini-live-api/SKILL.md)
