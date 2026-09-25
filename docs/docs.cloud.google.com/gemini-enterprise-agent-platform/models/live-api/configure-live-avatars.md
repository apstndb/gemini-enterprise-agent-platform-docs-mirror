---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-live-avatars
title: Configure live avatars
description: Learn how to configure live avatars in Gemini Live API.
data_source: docs.cloud.google.com
---

This document describes how to configure live avatars in Gemini Live API. Live avatars lets you generate real-time video of a talking avatar synchronized with synthesized speech responses from the `gemini-3.8-live` model. You can choose from a variety of built-in avatars and pair them with supported prebuilt voices in both Google Cloud console and Gemini Live API.

[Video](https://www.youtube.com/watch?v=oVG-5BF-dWo)

## Configure live avatars in Google Cloud console

Do the following:

1.  In the Google Cloud console, go to the **[Agent Platform \> Studio \> Stream realtime](https://console.cloud.google.com/agent-platform/studio/multimodal-live)** page.

2.  Click mic **Switch model** .

3.  From the models list, select `gemini-3.8-live` .

4.  In the main panel, select **Live Avatar** .

5.  From the **Avatar** list, select an avatar.

6.  From the **Voice** list, select a voice.

7.  Optional: Add system instructions to guide the behavior and output.

8.  Optional: Enable the camera input to share video with Gemini Live API.

9.  In the main panel, click **Start Session** .

## Configure live avatars using the API

Do the following:

1.  In `generation_config` set `"response_modalities": ["VIDEO"]` .

2.  In the `avatar_config` object, specify the prebuilt avatar name.

3.  In the `speech_config` object, specify the prebuilt voice.

### WebSocket configuration

WebSocket connections are established with a standard WebSocket handshake. The endpoint is regional and uses OAuth 2.0 bearer tokens for authentication. The authentication token is typically passed in WebSocket headers, such as `Authorization: Bearer [ TOKEN ]` .

The following is a sample WebSocket configuration:

    import asyncio
    import json
    import websockets
    
    # Replace PROJECT_ID and LOCATION with your Project ID and location.
    PROJECT_ID = "PROJECT_ID"
    LOCATION = "LOCATION"
    
    # Authentication
    token_list = !gcloud auth application-default print-access-token
    ACCESS_TOKEN = token_list[0]
    
    # Configuration
    MODEL_ID = "gemini-3.8-live"
    MODEL = f"projects/{PROJECT_ID}/locations/{LOCATION}/publishers/google/models/{MODEL_ID}"
    
    config = {
        "response_modalities": ["VIDEO"],
        "speech_config": {
            "voice_config": {
                "prebuilt_voice_config": {
                    "voice_name": "Puck",
                }
            }
        },
    }
    
    avatar_config = {
        "avatar_name": "Ben",
    }
    
    # Construct the WSS URL
    HOST = f"{LOCATION}-aiplatform.googleapis.com"
    URI = f"wss://{HOST}/ws/google.cloud.aiplatform.v1.LlmBidiService/BidiGenerateContent"
    
    async def main():
        headers = {"Authorization": f"Bearer {ACCESS_TOKEN}"}
    
        async with websockets.connect(URI, additional_headers=headers) as ws:
            print("Session established.")
    
            # Send Setup (Handshake)
            await ws.send(json.dumps({
                "setup": {
                    "model": MODEL,
                    "generation_config": config,
                    "avatar_config": avatar_config,
                }
            }))
            # Send and receive audio/video streams...
    
    if __name__ == "__main__":
        asyncio.run(main())

### Python SDK configuration

The following sample shows how to configure live avatars using the Google Gen AI SDK:

    from google import genai
    from google.genai import types
    
    client = genai.Client()
    
    config = types.LiveConnectConfig(
        response_modalities=["VIDEO"],
        speech_config=types.SpeechConfig(
            voice_config=types.VoiceConfig(
                prebuilt_voice_config=types.PrebuiltVoiceConfig(
                    voice_name="Puck",
                )
            )
        ),
        avatar_config=types.AvatarConfig(
            avatar_name="Ben",
        ),
        system_instruction=types.Content(
            parts=[types.Part.from_text(text="You are a helpful customer service assistant.")]
        ),
    )
    
    async with client.aio.live.connect(model="gemini-3.8-live", config=config) as session:
        # Interact with the live session...
        pass

## Use a custom avatar

Instead of choosing a prebuilt avatar, you can provide a reference image of a face, and Gemini Live API generates the avatar video from that likeness. Custom avatars are configured per session in the `customized_avatar` field of `avatar_config` .

> Custom avatars are only available to select customers. To request access, reach out to your Google Cloud account team. You are responsible for securing all consents and rights necessary for the processing of face and/or voice samples. When using this feature, you must comply with the [GenAI Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) , the [Google Cloud Acceptable Use Policy](https://cloud.google.com/terms/aup?e=48754805) , and the agreement under which you access and use Google Cloud services, including Section 32 of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) .

### Reference image requirements

The reference image must meet the following specifications:

  - **Image format** : PNG recommended. PNG uses lossless compression, and alpha transparency prevents a visible box around the avatar in light and dark modes.
  - **Color mode** : RGB.
  - **Image size** : 704 x 1280 pixels minimum (portrait).
  - **Resolution** : 720p or higher.
  - **Aspect ratio** : 9:16 (portrait) is standard. Landscape is also supported.
  - **File size** : Less than 5 MB
  - **Quality** : No blur or compression artifacts.

For the best results, also follow these composition guidelines:

  - **Framing:** Use a bust shot, where the head and shoulders occupy more than 60% of the frame. Crop out the lower body, arms, hands, and any held objects such as microphones or phones.

  - **Background:** Use a simple, uncluttered backdrop with no other people or distinct objects.

  - **Perspective:** Face the camera directly, with the head level and the eyes looking into the lens.

  - **Expression:** Keep the expression neutral and at rest, with no smiling, squinting, or visible teeth.

  - **Safety:** Don't use images of minors, celebrities, or offensive content.

### Configure a custom avatar in Google Cloud console

Do the following:

1.  In the Google Cloud console, go to the **[Agent Platform \> Studio \> Stream realtime](https://console.cloud.google.com/agent-platform/studio/multimodal-live)** page.

2.  From the models list, select `gemini-3.8-live` .

3.  In the main panel, click **Live Avatar** .

4.  Select Upload under the Avatar's options and upload an avatar image.

5.  Click **Start Session** , and then click **Start conversation** .

### Configure a custom avatar using the API

Configure the custom avatar in the initial `setup` payload that you send over the WebSocket connection:

    import base64
    import json
    import websockets
    
    # Load custom avatar image (PNG format, 704x1280 min)
    with open("/path/to/your/sample_avatar.png", "rb") as f:
        avatar_b64 = base64.b64encode(f.read()).decode("utf-8")
    
    GENERATION_CONFIG = {
        "response_modalities": ["VIDEO"],
    }
    
    # Setup avatar config with custom face image
    AVATAR_CONFIG = {
        "customized_avatar": {
            "image_data": avatar_b64,
            "image_mime_type": "png",
        }
    }
    
    # Session setup message
    SETUP_MESSAGE = {
        "setup": {
            "model": "gemini-3.8-live",
            "generation_config": GENERATION_CONFIG,
            "avatar_config": AVATAR_CONFIG,
            "system_instruction": {
                "parts": [{"text": "Your system instruction here"}]
            },
            "input_audio_transcription": {},
            "output_audio_transcription": {},
        }
    }

The preceding sample uses the following fields:

| Field path                                        | Type           | Description                                               |
| ------------------------------------------------- | -------------- | --------------------------------------------------------- |
| `generation_config.response_modalities`           | `list[string]` | Must be set to `["VIDEO"]` to enable avatar video output. |
| `avatar_config.customized_avatar.image_data`      | `string`       | Base64-encoded image string.                              |
| `avatar_config.customized_avatar.image_mime_type` | `string`       | Image MIME format ( `"png"` ).                            |

You can pair a custom avatar with a prebuilt voice or with a [custom voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-language-voice#custom-voice) .

## Available prebuilt voices

You can pair prebuilt avatars with any of the prebuilt HD voices in Gemini Live API. For more information on prebuilt voices, see [Prebuilt voices](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-language-voice#prebuilt-voice) .

## What's next

  - [Configure language and voice](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-language-voice)
  - [Start and manage live sessions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session)
  - [Send audio and video streams](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/send-audio-video-streams)
  - [Best practices with Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/best-practices)
