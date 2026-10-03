---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live
title: Gemini Live API reference
description: Reference documentation for the Gemini Live API, enabling low-latency bidirectional voice and video interactions with Gemini.
data_source: docs.cloud.google.com
---

> To try a tutorial that lets you use your voice and camera to talk to Gemini through the Gemini Live API, see the [`websocket-demo-app` tutorial](https://github.com/GoogleCloudPlatform/generative-ai/tree/main/gemini/multimodal-live-api/websocket-demo-app) .

The Gemini Live API enables low-latency bidirectional voice and video interactions with Gemini. Using the Gemini Live API, you can provide end users with the experience of natural, human-like voice conversations, and with the ability to interrupt the model's responses using voice commands. The Gemini Live API can process text, audio, and video input, and it can provide text and audio output.

For more information about the Gemini Live API, see [Gemini Live API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api) .

## Capabilities

Gemini Live API includes the following key capabilities:

- **Multimodality** : The model can see, hear, and speak.
- **Low-latency realtime interaction** : The model can provide fast responses.
- **Session memory** : The model retains memory of all interactions within a single session, recalling previously heard or seen information.
- **Support for function calling, code execution, and Search as a Tool** : You can integrate the model with external services and data sources.

Gemini Live API is designed for server-to-server communication.

For web and mobile apps, we recommend using the integration from our partners at [Daily](https://www.daily.co/products/gemini/multimodal-live-api/) .

## Supported models

#### Click to expand supported models

- [Gemini 3.8 Live](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-live)
- [Gemini 3.5 Transcribe](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-transcribe)
- [Gemini 3.5 Live Translate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-live-translate) preview
- [Gemini 2.5 Flash with Gemini Live API native audio](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/2-5-flash-live-api)

## Integration guide

This section describes how integration works with Gemini Live API.

### Sessions

A WebSocket connection establishes a session between the client and the Gemini server.

After a client initiates a new connection the session can exchange messages with the server to:

- Send text, audio, or video to the Gemini server.
- Receive audio, text, or function call requests from the Gemini server.

The session configuration is sent in the first message after connection. A session configuration includes the model, generation parameters, system instructions, and tools.

See the following example configuration:

```json
{
  "model": string,
  "generationConfig": {
    "candidateCount": integer,
    "maxOutputTokens": integer,
    "temperature": number,
    "topP": number,
    "topK": integer,
    "presencePenalty": number,
    "frequencyPenalty": number,
    "responseModalities": [string],
    "speechConfig": object
  },

  "systemInstruction": string,
  "tools": [object]
}
```

For more information, see [BidiGenerateContentSetup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#bidigeneratecontentsetup) .

### Send messages

Messages are JSON-formatted objects exchanged over the WebSocket connection.

To send a message the client must send a JSON object over an open WebSocket connection. The JSON object must have *exactly one* of the fields from the following object set:

```json
{
  "setup": BidiGenerateContentSetup,
  "clientContent": BidiGenerateContentClientContent,
  "realtimeInput": BidiGenerateContentRealtimeInput,
  "toolResponse": BidiGenerateContentToolResponse
}
```

#### Supported client messages

See the supported client messages in the following table:

| Message                            | Description                                                                      |
|------------------------------------|----------------------------------------------------------------------------------|
| `BidiGenerateContentSetup`         | Session configuration to be sent in the first message                            |
| `BidiGenerateContentClientContent` | Incremental content update of the current conversation delivered from the client |
| `BidiGenerateContentRealtimeInput` | Real time audio or video input                                                   |
| `BidiGenerateContentToolResponse`  | Response to a `ToolCallMessage` received from the server                         |

### Receive messages

To receive messages from Gemini, listen for the WebSocket 'message' event, and then parse the result according to the definition of the supported server messages.

See the following:

```
ws.addEventListener("message", async (evt) => {
  if (evt.data instanceof Blob) {
    // Process the received data (audio, video, etc.)
  } else {
    // Process JSON response
  }
});
```

Server messages will have *exactly one* of the fields from the following object set:

```json
{
  "setupComplete": BidiGenerateContentSetupComplete,
  "serverContent": BidiGenerateContentServerContent,
  "toolCall": BidiGenerateContentToolCall,
  "toolCallCancellation": BidiGenerateContentToolCallCancellation
  "usageMetadata": UsageMetadata
  "goAway": GoAway
  "sessionResumptionUpdate": SessionResumptionUpdate
  "inputTranscription": BidiGenerateContentTranscription
  "outputTranscription": BidiGenerateContentTranscription
}
```

#### Supported server messages

See the supported server messages in the following table:

| Message                                   | Description                                                                                     |
|-------------------------------------------|-------------------------------------------------------------------------------------------------|
| `BidiGenerateContentSetupComplete`        | A `BidiGenerateContentSetup` message from the client, sent when setup is complete               |
| `BidiGenerateContentServerContent`        | Content generated by the model in response to a client message                                  |
| `BidiGenerateContentToolCall`             | Request for the client to run the function calls and return the responses with the matching IDs |
| `BidiGenerateContentToolCallCancellation` | Sent when a function call is canceled due to the user interrupting model output                 |
| `UsageMetadata`                           | A report of the number of tokens used by the session so far                                     |
| `GoAway`                                  | A signal that the current connection will soon be terminated                                    |
| `SessionResumptionUpdate`                 | A session checkpoint, which can be resumed                                                      |
| `BidiGenerateContentTranscription`        | A transcription of either the user's or model's speech                                          |

### Incremental content updates

Use incremental updates to send text input, establish session context, or restore session context. For short contexts you can send turn-by-turn interactions to represent the exact sequence of events. For longer contexts it's recommended to provide a single message summary to free up the context window for the follow up interactions.

See the following example context message:

```
{
  "clientContent": {
    "turns": [
      {
          "parts":[
          {
            "text": ""
          }
        ],
        "role":"user"
      },
      {
          "parts":[
          {
            "text": ""
          }
        ],
        "role":"model"
      }
    ],
    "turnComplete": true
  }
}
```

Note that while content parts can be of a `functionResponse` type, `BidiGenerateContentClientContent` shouldn't be used to provide a response to the function calls issued by the model. `BidiGenerateContentToolResponse` should be used instead. `BidiGenerateContentClientContent` should only be used to establish previous context or provide text input to the conversation.

### Streaming audio and video

> To see an example of how to use the Gemini Live API in a streaming audio and video format, run the "Getting Started with the Gemini Live API using the Google Gen AI SDK" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api_genai_sdk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_multimodal_live_api_genai_sdk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_multimodal_live_api_genai_sdk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api_genai_sdk.ipynb)

### Code execution

> To see an example of code execution, run the "Intro to Generating and Executing Python Code with Gemini 3" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/code-execution/intro_code_execution.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fcode-execution%2Fintro_code_execution.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fcode-execution%2Fintro_code_execution.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/code-execution/intro_code_execution.ipynb)

To learn more about code execution, see [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution) .

### Function calling

> To see an example of function calling, run the "Intro to Function Calling with the Gemini API" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/function-calling/intro_function_calling.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Ffunction-calling%2Fintro_function_calling.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Ffunction-calling%2Fintro_function_calling.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/function-calling/intro_function_calling.ipynb)

All functions must be declared at the start of the session by sending tool definitions as part of the `BidiGenerateContentSetup` message.

You define functions by using JSON, specifically with a [select subset](https://ai.google.dev/api/caching#schema) of the [OpenAPI schema format](https://spec.openapis.org/oas/v3.0.3#schemawr) . A single function declaration can include the following parameters:

- **name** (string): The unique identifier for the function within the API call.

- **description** (string): A comprehensive explanation of the function's purpose and capabilities.

- **parameters** (object): Defines the input data required by the function.

  - **type** (string): Specifies the overall data type, such as object.

  - **properties** (object): Lists individual parameters, each with:

    - **type** (string): The data type of the parameter, such as string, integer, boolean.
    - **description** (string): A clear explanation of the parameter's purpose and expected format.

  - **required** (array): An array of strings listing the parameter names that are mandatory for the function to operate.

For code examples of a function declaration using curl commands, see [Function calling with the Gemini API](https://ai.google.dev/gemini-api/docs/function-calling#function-calling-curl-samples) . For examples of how to create function declarations using the Gemini API SDKs, see the [Function calling tutorial](https://ai.google.dev/gemini-api/docs/function-calling/tutorial) .

From a single prompt, the model can generate multiple function calls and the code necessary to chain their outputs. This code executes in a sandbox environment, generating subsequent `BidiGenerateContentToolCall` messages. The execution pauses until the results of each function call are available, which ensures sequential processing.

The client should respond with `BidiGenerateContentToolResponse` .

To learn more, see [Introduction to function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .

### Audio formats

See the list of [supported audio formats](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api#supported-audio-formats) .

### System instructions

You can provide system instructions to better control the model's output and specify the tone and sentiment of audio responses.

System instructions are added to the prompt before the interaction begins and remain in effect for the entire session.

System instructions can only be set at the beginning of a session, immediately following the initial connection. To provide further input to the model during the session, use incremental content updates.

### Interruptions

Users can interrupt the model's output at any time. When Voice activity detection (VAD) detects an interruption, the ongoing generation is canceled and discarded. Only the information already sent to the client is retained in the session history. The server then sends a `BidiGenerateContentServerContent` message to report the interruption.

In addition, the Gemini server discards any pending function calls and sends a `BidiGenerateContentServerContent` message with the IDs of the canceled calls.

### Voices

To specify a voice, set the `voiceName` within the `speechConfig` object, as part of your [session configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#sessions) .

See the following JSON representation of a `speechConfig` object:

```
{
  "voiceConfig": {
    "prebuiltVoiceConfig": {
      "voiceName": "VOICE_NAME"
    }
  }
}
```

To see the list of supported voices, see [Change voice and language settings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api#voice-settings) .

## Limitations

Consider the following limitations of Gemini Live API and Gemini 2.0 when you plan your project.

### Client authentication

Gemini Live API only provides server to server authentication and isn't recommended for direct client use. Client input should be routed through an intermediate application server for secure authentication with the Gemini Live API.

### Maximum session duration

The default maximum length of a conversation session is 10 minutes. For more information, see [Session length](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api#session_length) .

### Video frame rate

When you stream video to the model, it is processed at 1 frame per second (FPS). This makes the API unsuitable for use cases that require analyzing fast-changing video, such as play-by-play in high-speed sports.

### Voice activity detection (VAD)

By default, the model automatically performs voice activity detection (VAD) on a continuous audio input stream. VAD can be configured with the [`RealtimeInputConfig.AutomaticActivityDetection`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#google.cloud.aiplatform.v1beta1.RealtimeInputConfig.FIELDS.google.cloud.aiplatform.v1beta1.RealtimeInputConfig.AutomaticActivityDetection.google.cloud.aiplatform.v1beta1.RealtimeInputConfig.automatic_activity_detection) field of the [setup message](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#bidigeneratecontentsetup) .

When the audio stream is paused for more than a second (for example, when the user switches off the microphone), an `AudioStreamEnd` event is sent to flush any cached audio. The client can resume sending audio data at any time.

Alternatively, the automatic VAD can be turned off by setting `RealtimeInputConfig.AutomaticActivityDetection.disabled` to `true` in the setup message. In this configuration the client is responsible for detecting user speech and sending [`ActivityStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.FIELDS.google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.ActivityStart.google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.activity_start) and [`ActivityEnd`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live#google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.FIELDS.google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.ActivityEnd.google.cloud.aiplatform.v1beta1.BidiGenerateContentRealtimeInput.activity_end) messages at the appropriate times. An `AudioStreamEnd` isn't sent in this configuration. Instead, any interruption of the stream is marked by an `ActivityEnd` message.

### Additional limitations

Manual endpointing isn't supported.

Audio inputs and audio outputs negatively impact the model's ability to use function calling.

### Token count

Token count isn't supported.

### Rate limits

The following rate limits apply:

- 5,000 concurrent sessions per project
- 4M tokens per minute

## Messages and events

### BidiGenerateContentClientContent

Incremental update of the current conversation delivered from the client. All the content here is unconditionally appended to the conversation history and used as part of the prompt to the model to generate content.

A message here will interrupt any current model generation.

| Fields          |                                                                                                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `turns[]`       | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Content) Optional. The content appended to the current conversation with the model. For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history and latest request. |
| `turn_complete` | `bool` Optional. If true, indicates that the server content generation should start with the currently accumulated prompt. Otherwise, the server will await additional messages before starting generation.                                                                                                                                                                                    |

### BidiGenerateContentContextUpdate

Updates to the context of the current session.

Only fields that are set will be updated.

Updates are guaranteed to be processed *in order* with the rest of the inputs.

| Fields               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tools`              | [`Tools`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentContextUpdate.Tools) Optional. An updated list of tools the model may use to generate the subsequent responses. If set, this list replaces the previously provided tools. The tools are part of the model preamble, so updating them invalidates the prefix cache. Clients should only update this field when strictly necessary as it might have a performance impact on the model generation. |
| `system_instruction` | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Content) Optional. Updated system instruction for the model. If set, overrides `BidiGenerateContentSetup.system_instruction` . The system instructions are part of the model preamble, so updating them invalidates the prefix cache. Clients should only update this field when strictly necessary as it might have a performance impact on the model generation.                                               |

### Tools

A wrapper around the list of tools.

This wrapper exists because a bare `repeated Tool` field cannot tell apart "not sending a tools update" from "clearing all tools": an unset repeated field and an empty repeated field look identical on the wire. Wrapping the list in a message adds a presence bit, so the two cases become: - `tools` field unset: no update; keep the previously provided tools. - `tools` field set (even with an empty list): replace the current tools with the provided list, which may be empty to clear all tools.

| Fields    |                                                                                                                                                                                                                                |
|-----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `tools[]` | [`Tool`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Tool) Optional. The list of tools the model may use to generate the next response. |

### BidiGenerateContentRealtimeInput

User input that is sent in real time.

This is different from `ClientContentUpdate` in a few ways:

- Can be sent continuously without interruption to model generation.
- If there is a need to mix data interleaved across the `ClientContentUpdate` and the `RealtimeUpdate` , server attempts to optimize for best response, but there are no guarantees.
- End of turn is not explicitly specified, but is rather derived from user activity (for example, end of speech).
- Even before the end of turn, the data is processed incrementally to optimize for a fast start of the response from the model.
- Is always assumed to be the user's input (cannot be used to populate conversation history).

| Fields             |                                                                                                                                                                                                                                                                                                                                        |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `media_chunks[]`   | [`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Blob) Optional. Inlined bytes data for media input.                                                                                                                                        |
| `audio`            | [`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Blob) Optional. These form the realtime audio input stream.                                                                                                                                |
| `video`            | [`Blob`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Blob) Optional. These form the realtime video input stream.                                                                                                                                |
| `activity_start`   | [`ActivityStart`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentRealtimeInput.ActivityStart) Optional. Marks the start of user activity. This can only be sent if automatic (i.e. server-side) activity detection is disabled. |
| `activity_end`     | [`ActivityEnd`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentRealtimeInput.ActivityEnd) Optional. Marks the end of user activity. This can only be sent if automatic (i.e. server-side) activity detection is disabled.       |
| `audio_stream_end` | `bool` Optional. Indicates that the audio stream has ended, e.g. because the microphone was turned off. This should only be sent when automatic activity detection is enabled (which is the default). The client can reopen the stream by sending an audio message.                                                                    |
| `text`             | `string` Optional. These form the realtime text input stream.                                                                                                                                                                                                                                                                          |

### ActivityEnd

This type has no fields.

Marks the end of user activity.

### ActivityStart

This type has no fields.

Only one of the fields in this message must be set at a time. Marks the start of user activity.

### BidiGenerateContentServerContent

Incremental server update generated by the model in response to client messages.

Content is generated as quickly as possible, and not in realtime. Clients may choose to buffer and play it out in realtime.

| Fields                        |                                                                                                                                                                                                                                                                                                                                                                                                            |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `turn_complete`               | `bool` Output only. If true, indicates that the model is done generating. Generation will only start in response to additional client messages. Can be set alongside `content` , indicating that the `content` is the last in the turn.                                                                                                                                                                    |
| `interrupted`                 | `bool` Output only. If true, indicates that a client message has interrupted current model generation. If the client is playing out the content in realtime, this is a good signal to stop and empty the current queue. If the client is playing out the content in realtime, this is a good signal to stop and empty the current playback queue.                                                          |
| `generation_complete`         | `bool` Output only. If true, indicates that the model is done generating. When model is interrupted while generating there will be no 'generation_complete' message in interrupted turn, it will go through 'interrupted \> turn_complete'. When model assumes realtime playback there will be delay between generation_complete and turn_complete that is caused by model waiting for playback to finish. |
| `grounding_metadata`          | [`GroundingMetadata`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.GroundingMetadata) Output only. Metadata specifies sources used to ground generated content.                                                                                                                                                      |
| `input_transcription`         | [`Transcription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.Transcription) Optional. Input transcription. The transcription is independent of the model turn, which means it does not imply any ordering between transcription and model turn.                                   |
| `output_transcription`        | [`Transcription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.Transcription) Optional. Output transcription. The transcription is independent of the model turn, which means it does not imply any ordering between transcription and model turn.                                  |
| `turn_complete_reason`        | [`TurnCompleteReason`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.TurnCompleteReason) Output only. The reason why the turn is complete.                                                                                                                                           |
| `speech_state`                | [`SpeechState`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.SpeechState) Output only. Indicates the current state of speech detection on `realtime_input.audio` . Not set or zero if the state is unchanged.                                                                       |
| `interim_input_transcription` | [`Transcription`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.Transcription) Optional. Low-latency interim transcription updated while the user is speaking.                                                                                                                       |
| `interaction_status`          | [`InteractionStatus`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentServerContent.InteractionStatus) Output only. The current activity status of the live session. Always sent alongside `turn_complete` .                                                                                         |
| `model_turn`                  | [`Content`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Content) Output only. The content that the model has generated as part of the current conversation with the user.                                                                                                                                           |

### InteractionStatus

The different activity states of the live session. This field is always sent together with `turn_complete` to indicate whether the server has finished all processing.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Enums</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>INTERACTION_STATUS_UNSPECIFIED</code></td>
<td>Unspecified interaction status.</td>
</tr>
<tr class="even">
<td><code>IN_PROGRESS</code></td>
<td>The server is still actively processing user input or running background reasoning. More model output may follow.</td>
</tr>
<tr class="odd">
<td><code>REQUIRES_ACTION</code></td>
<td><p>Deprecated: Use IDLE instead. The server has completed all processing and background reasoning.</p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote></td>
</tr>
<tr class="even">
<td><code>IDLE</code></td>
<td>The server has completed all processing and background reasoning.</td>
</tr>
</tbody>
</table>

### SpeechState

The different states of server-side speech detection.

| Enums                      |                                                                                                 |
|----------------------------|-------------------------------------------------------------------------------------------------|
| `SPEECH_STATE_UNSPECIFIED` | Unspecified speech state. If the speech state is changing, one of the other values will be set. |
| `NON_SPEECH`               | No speech detected.                                                                             |
| `SPEECH`                   | Speech detected.                                                                                |

### Transcription

Audio transcription message.

| Fields     |                                                                   |
|------------|-------------------------------------------------------------------|
| `text`     | `string` Optional. The transcription text.                        |
| `finished` | `bool` Optional. Indicates whether the transcription is complete. |

### TurnCompleteReason

The reason why the turn is complete.

| Enums                                                   |                                                                                                                                                                  |
|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `TURN_COMPLETE_REASON_UNSPECIFIED`                      | Reason is unspecified.                                                                                                                                           |
| `MALFORMED_FUNCTION_CALL`                               | The function call generated by the model is invalid.                                                                                                             |
| `RESPONSE_REJECTED`                                     | The response is rejected by the model.                                                                                                                           |
| `NEED_MORE_INPUT`                                       | Needs more input from the user.                                                                                                                                  |
| `PROHIBITED_INPUT_CONTENT`                              | Input safety related finish reasons. Replicated from learning/genai/beyond/recipe_runner/finish_reason.proto:FinishReason. Input content is prohibited.          |
| `IMAGE_PROHIBITED_INPUT_CONTENT`                        | Input image contains prohibited content.                                                                                                                         |
| `INPUT_TEXT_CONTAIN_PROMINENT_PERSON_PROHIBITED`        | Input text contains prominent person reference.                                                                                                                  |
| `INPUT_IMAGE_CELEBRITY`                                 | Input image contains celebrity.                                                                                                                                  |
| `INPUT_IMAGE_PHOTO_REALISTIC_CHILD_PROHIBITED`          | Input image contains photo realistic child.                                                                                                                      |
| `INPUT_TEXT_NCII_PROHIBITED`                            | Input text contains NCII content.                                                                                                                                |
| `INPUT_OTHER`                                           | Other input safety issue.                                                                                                                                        |
| `INPUT_IP_PROHIBITED`                                   | Input contains IP violation.                                                                                                                                     |
| `BLOCKLIST`                                             | Input matched blocklist.                                                                                                                                         |
| `UNSAFE_PROMPT_FOR_IMAGE_GENERATION`                    | Input is unsafe for image generation.                                                                                                                            |
| `GENERATED_IMAGE_SAFETY`                                | Output safety related finish reasons. Replicated from learning/genai/beyond/recipe_runner/finish_reason.proto:FinishReason. Generated image failed safety check. |
| `GENERATED_CONTENT_SAFETY`                              | Generated content failed safety check.                                                                                                                           |
| `GENERATED_AUDIO_SAFETY`                                | Generated audio failed safety check.                                                                                                                             |
| `GENERATED_VIDEO_SAFETY`                                | Generated video failed safety check.                                                                                                                             |
| `GENERATED_CONTENT_PROHIBITED`                          | Generated content is prohibited.                                                                                                                                 |
| `GENERATED_CONTENT_BLOCKLIST`                           | Generated content matched blocklist.                                                                                                                             |
| `GENERATED_IMAGE_PROHIBITED`                            | Generated image is prohibited.                                                                                                                                   |
| `GENERATED_IMAGE_CELEBRITY`                             | Generated image contains celebrity.                                                                                                                              |
| `GENERATED_IMAGE_PROMINENT_PEOPLE_DETECTED_BY_REWRITER` | Generated image contains prominent people detected by rewriter.                                                                                                  |
| `GENERATED_IMAGE_IDENTIFIABLE_PEOPLE`                   | Generated image contains identifiable people.                                                                                                                    |
| `GENERATED_IMAGE_MINORS`                                | Generated image contains minors.                                                                                                                                 |
| `OUTPUT_IMAGE_IP_PROHIBITED`                            | Generated image contains IP violation.                                                                                                                           |
| `GENERATED_OTHER`                                       | Other generated content issue.                                                                                                                                   |
| `MAX_REGENERATION_REACHED`                              | Max regeneration attempts reached.                                                                                                                               |

### BidiGenerateContentSetup

Message to be sent in the first and only first client message. Contains configuration that will apply for the duration of the streaming session.

Clients should wait for a `BidiGenerateContentSetupComplete` message before sending any additional messages.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>model</code></td>
<td><p><code>string</code></p>
<p>Required. The fully qualified name of the publisher model.</p>
<p>Publisher model format: <code>projects/{project}/locations/{location}/publishers/\*/models/\*</code></p></td>
</tr>
<tr class="even">
<td><code>generation_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.GenerationConfig"><code>GenerationConfig</code></a></p>
<p>Optional. Generation config.</p>
<p>The following fields aren't supported:</p>
<ul>
<li><code>response_logprobs</code></li>
<li><code>response_mime_type</code></li>
<li><code>logprobs</code></li>
<li><code>response_schema</code></li>
<li><code>stop_sequence</code></li>
<li><code>routing_config</code></li>
<li><code>audio_timestamp</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><code>system_instruction</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Content"><code>Content</code></a></p>
<p>Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.</p></td>
</tr>
<tr class="even">
<td><code>tools[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.Tool"><code>Tool</code></a></p>
<p>Optional. A list of <code>Tools</code> the model may use to generate the next response.</p>
<p>A <code>Tool</code> is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.</p></td>
</tr>
<tr class="odd">
<td><code>session_resumption</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.SessionResumptionConfig"><code>SessionResumptionConfig</code></a></p>
<p>Optional. Configures session resumption mechanism. If included, the server will send periodical <code>SessionResumptionUpdate</code> messages to the client.</p></td>
</tr>
<tr class="even">
<td><code>context_window_compression</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.ContextWindowCompressionConfig"><code>ContextWindowCompressionConfig</code></a></p>
<p>Optional. Configures context window compression mechanism.</p>
<p>If included, server will compress context window to fit into given length.</p></td>
</tr>
<tr class="odd">
<td><code>realtime_input_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.RealtimeInputConfig"><code>RealtimeInputConfig</code></a></p>
<p>Optional. Configures the handling of realtime input.</p></td>
</tr>
<tr class="even">
<td><code>input_audio_transcription</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentSetup.AudioTranscriptionConfig"><code>AudioTranscriptionConfig</code></a></p>
<p>Optional. Configures transcription of the input audio, which aligns with the input audio language.</p></td>
</tr>
<tr class="odd">
<td><code>output_audio_transcription</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentSetup.AudioTranscriptionConfig"><code>AudioTranscriptionConfig</code></a></p>
<p>Optional. Configures transcription of the output audio, which aligns with the language code specified for the output audio.</p></td>
</tr>
<tr class="even">
<td><code>explicit_vad_signal</code></td>
<td><p><code>bool</code></p>
<p>Optional. Indicates whether the server sends the built-in VAD signal to the user.</p></td>
</tr>
<tr class="odd">
<td><code>proactivity</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.ProactivityConfig"><code>ProactivityConfig</code></a></p>
<p>Optional. Configures the proactivity of the model.</p>
<p>This allows the model to respond proactively to the input and to ignore irrelevant input.</p></td>
</tr>
<tr class="even">
<td><code>avatar_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.AvatarConfig"><code>AvatarConfig</code></a></p>
<p>Optional. Config for video generation.</p></td>
</tr>
<tr class="odd">
<td><code>safety_settings[]</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.SafetySetting"><code>SafetySetting</code></a></p>
<p>Optional. List of safety settings to use for blocking unsafe content.</p></td>
</tr>
<tr class="even">
<td><code>history_config</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.HistoryConfig"><code>HistoryConfig</code></a></p>
<p>Optional. Configuration for the conversation history.</p></td>
</tr>
<tr class="odd">
<td><code>labels</code></td>
<td><p><code>map&lt;string, string&gt;</code></p>
<p>Optional. The labels with user-defined metadata for the request. It is used for billing and reporting only.</p>
<p>Label keys and values can be no longer than 63 characters (Unicode codepoints) and can only contain lowercase letters, numeric characters, underscores, and dashes. International characters are allowed. Label values are optional. Label keys must start with a letter.</p></td>
</tr>
</tbody>
</table>

### AudioTranscriptionConfig

The audio transcription configuration.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>language_codes[]</code></td>
<td><p><code>string</code></p>
<p>Optional. BCP-47 language codes providing hints about the languages present in the audio. If omitted or empty, defaults to automatic language detection.</p></td>
</tr>
<tr class="even">
<td><code>adaptation_phrases[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use <code>custom_vocabulary</code> instead. A list of phrases used for speech adaptation, which biases the speech recognition model to improve recognition of these specific terms.</p></td>
</tr>
<tr class="odd">
<td><code>custom_vocabulary[]</code></td>
<td><p><code>string</code></p>
<p>Optional. A list of custom vocabulary phrases to bias the speech recognition model toward recognizing specific terms.</p></td>
</tr>
<tr class="even">
<td><code>mode</code></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentSetup.AudioTranscriptionConfig.Mode"><code>Mode</code></a></p>
<p>Optional. Configures transcription mode. Supported values: <code>VERBATIM</code> , <code>SMART</code> . If unspecified, defaults to <code>VERBATIM</code> transcription. In <code>SMART</code> mode, the model performs disfluency removal (eliminating filler words, repetitions, and false starts), light grammatical cleanup, automatic formatting (paragraphs, bullet points, numbered lists), and minor user edits (inline self-corrections). Timestamps and diarization are incompatible with mode <code>SMART</code> .</p></td>
</tr>
<tr class="odd">
<td>Union field <code>language_config</code> . Deprecated: Use top-level <code>language_codes</code> instead. <code>language_config</code> can be only one of the following:</td>
<td></td>
</tr>
<tr class="even">
<td><code>language_auto </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentSetup.AudioTranscriptionConfig.LanguageAuto"><code>LanguageAuto</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use top-level <code>language_codes</code> instead. The model will detect the language automatically.</p></td>
</tr>
<tr class="odd">
<td><code>language_hints </code><strong><code>(deprecated)</code></strong></td>
<td><p><a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.BidiGenerateContentSetup.AudioTranscriptionConfig.LanguageHints"><code>LanguageHints</code></a></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Optional. Deprecated: Use top-level <code>language_codes</code> instead. Specifies one or more languages in the audio.</p></td>
</tr>
</tbody>
</table>

### LanguageAuto

This type has no fields.

> This item is deprecated!

Deprecated: Use top-level `language_codes` instead. Indicates the language of the audio should be automatically detected.

### LanguageHints

> This item is deprecated!

Deprecated: Use top-level `language_codes` instead. Provides hints to the model about possible languages present in the audio.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Fields</th>
<th></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>language_codes[] </code><strong><code>(deprecated)</code></strong></td>
<td><p><code>string</code></p>
<blockquote>
<p>This item is deprecated!</p>
</blockquote>
<p>Required. Deprecated: Use top-level <code>language_codes</code> instead. BCP-47 language codes. At least one must be specified.</p></td>
</tr>
</tbody>
</table>

### Mode

Transcription mode.

| Enums              |                                 |
|--------------------|---------------------------------|
| `MODE_UNSPECIFIED` | Unspecified transcription mode. |
| `VERBATIM`         | Verbatim transcription mode.    |
| `SMART`            | Smart transcription mode.       |

### BidiGenerateContentSetupComplete

Sent in response to a `BidiGenerateContentSetup` message from the client.

| Fields       |                                                      |
|--------------|------------------------------------------------------|
| `session_id` | `string` Output only. The session id of the session. |

### BidiGenerateContentToolCall

Request for the client to execute the `function_calls` and return the responses with the matching `id` s.

| Fields             |                                                                                                                                                                                                                  |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `function_calls[]` | [`FunctionCall`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.FunctionCall) Output only. The function call to be executed. |

### BidiGenerateContentToolCallCancellation

Notification for the client that a previously issued `ToolCallMessage` with the specified `id` s should have been not executed and should be cancelled. If there were side-effects to those tool calls, clients may attempt to undo the tool calls. This message occurs only in cases where the clients interrupt server turns.

| Fields  |                                                                  |
|---------|------------------------------------------------------------------|
| `ids[]` | `string` Output only. The ids of the tool calls to be cancelled. |

### BidiGenerateContentToolResponse

Client generated response to a `ToolCall` received from the server. Individual `FunctionResponse` objects are matched to the respective `FunctionCall` objects by the `id` field.

Note that in the unary and server-streaming GenerateContent APIs function calling happens by exchanging the `Content` parts, while in the bidi GenerateContent APIs function calling happens over these dedicated set of messages.

| Fields                 |                                                                                                                                                                                                                         |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `function_responses[]` | [`FunctionResponse`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rpc/google.cloud.aiplatform.v1#google.cloud.aiplatform.v1.FunctionResponse) Optional. The response to the function calls. |

## What's next

- Get started with the Gemini Live API using the [Google Gen AI SDK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/get-started-sdk) , [WebSockets](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/get-started-websocket) , or [ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/get-started-adk) .
- Learn more about [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .
- For examples, see the [Function calling reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling) .
