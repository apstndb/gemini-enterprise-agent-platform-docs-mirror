---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/multimodal-live
title: Gemini Live API reference
description: Reference documentation for the Gemini Live API, enabling low-latency bidirectional voice and video interactions with Gemini.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> To try a tutorial that lets you use your voice and camera to talk to Gemini through the Gemini Live API, see the [`websocket-demo-app` tutorial](https://github.com/GoogleCloudPlatform/generative-ai/tree/main/gemini/multimodal-live-api/websocket-demo-app) .

[Video](https://www.youtube.com/watch?v=_vc8sXog2ek)

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

## Get started

To try the Gemini Live API, go to the [Agent Studio on Gemini Enterprise Agent Platform](https://console.cloud.google.com/agent-platform/studio/multimodal-live) , and then click **Start Session** .

Gemini Live API is a stateful API that uses [WebSockets](https://en.wikipedia.org/wiki/WebSocket) .

This section shows an example of how to use Gemini Live API for text-to-text generation, using Python 3.9+.

### Python

#### Install

    pip install --upgrade google-genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/python-genai/) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_VERTEXAI=True

    from google import genai
    from google.genai.types import (Content, HttpOptions, LiveConnectConfig,
                                    Modality, Part)
    
    client = genai.Client(http_options=HttpOptions(api_version="v1beta1"))
    model_id = "gemini-2.0-flash-live-preview-04-09"
    
    async with client.aio.live.connect(
        model=model_id,
        config=LiveConnectConfig(response_modalities=[Modality.TEXT]),
    ) as session:
        text_input = "Hello? Gemini, are you there?"
        print("> ", text_input, "\n")
        await session.send_client_content(
            turns=Content(role="user", parts=[Part(text=text_input)])
        )
    
        response = []
    
        async for message in session.receive():
            if message.text:
                response.append(message.text)
    
        print("".join(response))
    # Example output:
    # >  Hello? Gemini, are you there?
    # Yes, I'm here. What would you like to talk about?

### Go

Learn how to install or update the [Go](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://pkg.go.dev/google.golang.org/genai) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_VERTEXAI=True

    import (
        "context"
        "fmt"
        "io"
    
        "google.golang.org/genai"
    )
    
    // generateLiveWithText demonstrates using a live Gemini model
    // that performs live with text and handles responses.
    func generateLiveWithText(w io.Writer) error {
        ctx := context.Background()
    
        client, err := genai.NewClient(ctx, &genai.ClientConfig{
            HTTPOptions: genai.HTTPOptions{APIVersion: "v1"},
        })
        if err != nil {
            return fmt.Errorf("failed to create genai client: %w", err)
        }
    
        modelName := "gemini-2.0-flash-live-preview-04-09"
    
        config := &genai.LiveConnectConfig{
            ResponseModalities: []genai.Modality{genai.ModalityText},
        }
    
        // Open a live session
        session, err := client.Live.Connect(ctx, modelName, config)
        if err != nil {
            return fmt.Errorf("failed to connect live: %w", err)
        }
        defer session.Close()
    
        // Prepare the input message
        inputText := "Hello? Gemini, are you there?"
        fmt.Fprintf(w, "> %s\n\n", inputText)
    
        // Send text content to the model
        err = session.SendClientContent(genai.LiveClientContentInput{
            Turns: []*genai.Content{
                {
                    Role: genai.RoleUser,
                    Parts: []*genai.Part{
                        {Text: inputText},
                    },
                },
            },
        })
        if err != nil {
            return fmt.Errorf("failed to send content: %w", err)
        }
    
        // Stream the response
        var response string
        for {
            chunk, err := session.Receive()
            if err != nil {
                if err == io.EOF {
                    break
                }
                return fmt.Errorf("error receiving response: %w", err)
            }
    
            if chunk.ServerContent != nil && chunk.ServerContent.ModelTurn != nil {
                for _, part := range chunk.ServerContent.ModelTurn.Parts {
                    if part.Text != "" {
                        response += part.Text
                    }
                }
            }
        }
    
        // Example output:
        //  >  Hello? Gemini are you there?
        //  Yes, I'm here. What would you like to talk about?
        fmt.Fprintln(w, response)
        return nil
    }

### Node.js

#### Install

    npm install @google/genai

To learn more, see the [SDK reference documentation](https://googleapis.github.io/js-genai/) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_VERTEXAI=True

    'use strict';
    
    const {GoogleGenAI, Modality} = require('@google/genai');
    
    const GOOGLE_CLOUD_PROJECT = process.env.GOOGLE_CLOUD_PROJECT;
    const GOOGLE_CLOUD_LOCATION = process.env.GOOGLE_CLOUD_LOCATION || 'global';
    
    async function generateLiveConversation(
      projectId = GOOGLE_CLOUD_PROJECT,
      location = GOOGLE_CLOUD_LOCATION
    ) {
      const client = new GoogleGenAI({
        vertexai: true,
        project: projectId,
        location: location,
      });
    
      const modelId = 'gemini-2.0-flash-live-preview-04-09';
      const config = {responseModalities: [Modality.TEXT]};
    
      const responseQueue = [];
    
      async function waitMessage() {
        while (responseQueue.length === 0) {
          await new Promise(resolve => setTimeout(resolve, 100));
        }
        return responseQueue.shift();
      }
    
      async function handleTurn() {
        const turns = [];
        let done = false;
        while (!done) {
          const message = await waitMessage();
          turns.push(message);
          if (message.serverContent && message.serverContent.turnComplete) {
            done = true;
          }
        }
        return turns;
      }
    
      const session = await client.live.connect({
        model: modelId,
        config: config,
        callbacks: {
          onmessage: msg => responseQueue.push(msg),
          onerror: e => console.error('Error:', e.message),
        },
      });
    
      const textInput = 'Hello? Gemini, are you there?';
      console.log('> ', textInput, '\n');
    
      await session.sendClientContent({
        turns: [{role: 'user', parts: [{text: textInput}]}],
      });
    
      const turns = await handleTurn();
      for (const turn of turns) {
        if (turn.text) {
          console.log('Received text:', turn.text);
        }
      }
      // Example output:
      //> Hello? Gemini, are you there?
      // Received text: Yes
      // Received text: I'm here. How can I help you today?
      session.close();
      return turns;
    }

### Java

Learn how to install or update the [Java](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/sdks/overview) .

To learn more, see the [SDK reference documentation](https://central.sonatype.com/artifact/com.google.genai/google-genai) .

Set environment variables to use the Gen AI SDK with Vertex AI:

    # Replace the `GOOGLE_CLOUD_PROJECT` and `GOOGLE_CLOUD_LOCATION` values
    # with appropriate values for your project.
    export GOOGLE_CLOUD_PROJECT=GOOGLE_CLOUD_PROJECT
    export GOOGLE_CLOUD_LOCATION=global
    export GOOGLE_GENAI_USE_VERTEXAI=True

    import static com.google.genai.types.Modality.Known.TEXT;
    
    import com.google.genai.AsyncSession;
    import com.google.genai.Client;
    import com.google.genai.types.Content;
    import com.google.genai.types.HttpOptions;
    import com.google.genai.types.LiveConnectConfig;
    import com.google.genai.types.LiveSendClientContentParameters;
    import com.google.genai.types.LiveServerContent;
    import com.google.genai.types.LiveServerMessage;
    import com.google.genai.types.Part;
    import java.util.concurrent.CompletableFuture;
    
    public class LiveWithTxt {
    
      public static void main(String[] args) {
        // TODO(developer): Replace these variables before running the sample.
        String modelId = "gemini-2.0-flash-live-preview-04-09";
        generateContent(modelId);
      }
    
      // Shows how to send a text prompt and receive messages from the live session.
      public static String generateContent(String modelId) {
        // Client Initialization. Once created, it can be reused for multiple requests.
        try (Client client =
            Client.builder()
                .location("us-central1")
                .vertexAI(true)
                .httpOptions(HttpOptions.builder().apiVersion("v1beta1").build())
                .build()) {
    
          // Connects to the live server.
          CompletableFuture<AsyncSession> sessionFuture =
              client.async.live.connect(
                  modelId, LiveConnectConfig.builder().responseModalities(TEXT).build());
    
          // Sends and receives messages from the live session.
          CompletableFuture<String> responseFuture =
              sessionFuture.thenCompose(
                  session -> {
                    // A future that completes when the model signals the end of its turn.
                    CompletableFuture<Void> turnComplete = new CompletableFuture<>();
                    // A variable to concatenate the text response from the model.
                    StringBuilder modelResponse = new StringBuilder();
                    // Starts receiving messages from the live session.
                    session.receive(
                        message -> handleLiveServerMessage(message, turnComplete, modelResponse));
                    // Sends content to the live session and waits for the turn to complete.
                    return sendContent(session)
                        .thenCompose(unused -> turnComplete)
                        .thenCompose(
                            unused -> session.close().thenApply(result -> modelResponse.toString()));
                  });
    
          String response = responseFuture.join();
          System.out.println(response);
          // Example output:
          // > Hello? Gemini, are you there?
          //
          // Yes, I am here. How can I help you today?
          return response;
        }
      }
    
      // Sends content to the live session.
      private static CompletableFuture<Void> sendContent(AsyncSession session) {
        String textInput = "Hello? Gemini, are you there?";
        System.out.printf("> %s\n", textInput);
        return session.sendClientContent(
            LiveSendClientContentParameters.builder()
                .turns(Content.builder().role("user").parts(Part.fromText(textInput)).build())
                .turnComplete(true)
                .build());
      }
    
      // Concatenates the output transcription from the model and signals
      // `turnComplete` when the model is done generating the response.
      private static void handleLiveServerMessage(
          LiveServerMessage message, CompletableFuture<Void> turnComplete, StringBuilder response) {
        message
            .serverContent()
            .flatMap(LiveServerContent::modelTurn)
            .flatMap(Content::parts)
            .ifPresent(parts -> parts.forEach(part -> part.text().ifPresent(response::append)));
        // Checks if the model's turn is over.
        if (message.serverContent().flatMap(LiveServerContent::turnComplete).orElse(false)) {
          turnComplete.complete(null);
        }
      }
    }

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
| ---------------------------------- | -------------------------------------------------------------------------------- |
| `BidiGenerateContentSetup`         | Session configuration to be sent in the first message                            |
| `BidiGenerateContentClientContent` | Incremental content update of the current conversation delivered from the client |
| `BidiGenerateContentRealtimeInput` | Real time audio or video input                                                   |
| `BidiGenerateContentToolResponse`  | Response to a `ToolCallMessage` received from the server                         |

### Receive messages

To receive messages from Gemini, listen for the WebSocket 'message' event, and then parse the result according to the definition of the supported server messages.

See the following:

    ws.addEventListener("message", async (evt) => {
      if (evt.data instanceof Blob) {
        // Process the received data (audio, video, etc.)
      } else {
        // Process JSON response
      }
    });

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
| ----------------------------------------- | ----------------------------------------------------------------------------------------------- |
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

Note that while content parts can be of a `functionResponse` type, `BidiGenerateContentClientContent` shouldn't be used to provide a response to the function calls issued by the model. `BidiGenerateContentToolResponse` should be used instead. `BidiGenerateContentClientContent` should only be used to establish previous context or provide text input to the conversation.

### Streaming audio and video

> To see an example of how to use the Gemini Live API in a streaming audio and video format, run the "Getting Started with the Gemini Live API using the Gen AI SDK" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api_genai_sdk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_multimodal_live_api_genai_sdk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_multimodal_live_api_genai_sdk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_multimodal_live_api_genai_sdk.ipynb)

### Code execution

> To see an example of code execution, run the "Intro to Generating and Executing Python Code with Gemini 2.0" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/code-execution/intro_code_execution.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fcode-execution%2Fintro_code_execution.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fcode-execution%2Fintro_code_execution.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/code-execution/intro_code_execution.ipynb)

To learn more about code execution, see [Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/code-execution) .

### Function calling

> To see an example of function calling, run the "Intro to Function Calling with the Gemini API" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/function-calling/intro_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Ffunction-calling%2Fintro_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Ffunction-calling%2Fintro_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/function-calling/intro_function_calling.ipynb)

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

    {
      "voiceConfig": {
        "prebuiltVoiceConfig": {
          "voiceName": "VOICE_NAME"
        }
      }
    }

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

Fields

`turns[]`

`  Content  `

Optional. The content appended to the current conversation with the model.

For single-turn queries, this is a single instance. For multi-turn queries, this is a repeated field that contains conversation history and latest request.

`turn_complete`

`bool`

Optional. If true, indicates that the server content generation should start with the currently accumulated prompt. Otherwise, the server will await additional messages before starting generation.

### BidiGenerateContentRealtimeInput

User input that is sent in real time.

This is different from `ClientContentUpdate` in a few ways:

  - Can be sent continuously without interruption to model generation.
  - If there is a need to mix data interleaved across the `ClientContentUpdate` and the `RealtimeUpdate` , server attempts to optimize for best response, but there are no guarantees.
  - End of turn is not explicitly specified, but is rather derived from user activity (for example, end of speech).
  - Even before the end of turn, the data is processed incrementally to optimize for a fast start of the response from the model.
  - Is always assumed to be the user's input (cannot be used to populate conversation history).

Fields

`media_chunks[]`

`  Blob  `

Optional. Inlined bytes data for media input.

`activity_start`

`  ActivityStart  `

Optional. Marks the start of user activity. This can only be sent if automatic (i.e. server-side) activity detection is disabled.

`activity_end`

`  ActivityEnd  `

Optional. Marks the end of user activity. This can only be sent if automatic (i.e. server-side) activity detection is disabled.

### ActivityEnd

This type has no fields.

Marks the end of user activity.

### ActivityStart

This type has no fields.

Only one of the fields in this message must be set at a time. Marks the start of user activity.

### BidiGenerateContentServerContent

Incremental server update generated by the model in response to client messages.

Content is generated as quickly as possible, and not in realtime. Clients may choose to buffer and play it out in realtime.

Fields

`turn_complete`

`bool`

Output only. If true, indicates that the model is done generating. Generation will only start in response to additional client messages. Can be set alongside `content` , indicating that the `content` is the last in the turn.

`interrupted`

`bool`

Output only. If true, indicates that a client message has interrupted current model generation. If the client is playing out the content in realtime, this is a good signal to stop and empty the current queue. If the client is playing out the content in realtime, this is a good signal to stop and empty the current playback queue.

`generation_complete`

`bool`

Output only. If true, indicates that the model is done generating.

When model is interrupted while generating there will be no 'generation\_complete' message in interrupted turn, it will go through 'interrupted \> turn\_complete'.

When model assumes realtime playback there will be delay between generation\_complete and turn\_complete that is caused by model waiting for playback to finish.

`grounding_metadata`

`  GroundingMetadata  `

Output only. Metadata specifies sources used to ground generated content.

`input_transcription`

`  Transcription  `

Optional. Input transcription. The transcription is independent to the model turn which means it doesn't imply any ordering between transcription and model turn.

`output_transcription`

`  Transcription  `

Optional. Output transcription. The transcription is independent to the model turn which means it doesn't imply any ordering between transcription and model turn.

`model_turn`

`  Content  `

Output only. The content that the model has generated as part of the current conversation with the user.

### Transcription

Audio transcription message.

Fields

`text`

`string`

Optional. Transcription text.

`finished`

`bool`

Optional. The bool indicates the end of the transcription.

### BidiGenerateContentSetup

Message to be sent in the first and only first client message. Contains configuration that will apply for the duration of the streaming session.

Clients should wait for a `BidiGenerateContentSetupComplete` message before sending any additional messages.

Fields

`model`

`string`

Required. The fully qualified name of the publisher model.

Publisher model format: `projects/{project}/locations/{location}/publishers/\*/models/\*`

`generation_config`

`  GenerationConfig  `

Optional. Generation config.

The following fields aren't supported:

  - `response_logprobs`
  - `response_mime_type`
  - `logprobs`
  - `response_schema`
  - `stop_sequence`
  - `routing_config`
  - `audio_timestamp`

`system_instruction`

`  Content  `

Optional. The user provided system instructions for the model. Note: only text should be used in parts and content in each part will be in a separate paragraph.

`tools[]`

`  Tool  `

Optional. A list of `Tools` the model may use to generate the next response.

A `Tool` is a piece of code that enables the system to interact with external systems to perform an action, or set of actions, outside of knowledge and scope of the model.

`session_resumption`

`  SessionResumptionConfig  `

Optional. Configures session resumption mechanism. If included, the server will send periodical `SessionResumptionUpdate` messages to the client.

`context_window_compression`

`  ContextWindowCompressionConfig  `

Optional. Configures context window compression mechanism.

If included, server will compress context window to fit into given length.

`realtime_input_config`

`  RealtimeInputConfig  `

Optional. Configures the handling of realtime input.

`input_audio_transcription`

`  AudioTranscriptionConfig  `

Optional. The transcription of the input aligns with the input audio language.

`output_audio_transcription`

`  AudioTranscriptionConfig  `

Optional. The transcription of the output aligns with the language code specified for the output audio.

### AudioTranscriptionConfig

This type has no fields.

The audio transcription configuration.

### BidiGenerateContentSetupComplete

Sent in response to a `BidiGenerateContentSetup` message from the client.

Fields

`session_id`

`string`

The session id of the session.

### BidiGenerateContentToolCall

Request for the client to execute the `function_calls` and return the responses with the matching `id` s.

Fields

`function_calls[]`

`  FunctionCall  `

Output only. The function call to be executed.

### BidiGenerateContentToolCallCancellation

Notification for the client that a previously issued `ToolCallMessage` with the specified `id` s should have been not executed and should be cancelled. If there were side-effects to those tool calls, clients may attempt to undo the tool calls. This message occurs only in cases where the clients interrupt server turns.

Fields

`ids[]`

`string`

Output only. The ids of the tool calls to be cancelled.

### BidiGenerateContentToolResponse

Client generated response to a `ToolCall` received from the server. Individual `FunctionResponse` objects are matched to the respective `FunctionCall` objects by the `id` field.

Note that in the unary and server-streaming GenerateContent APIs function calling happens by exchanging the `Content` parts, while in the bidi GenerateContent APIs function calling happens over these dedicated set of messages.

Fields

`function_responses[]`

`  FunctionResponse  `

Optional. The response to the function calls.

## RealtimeInputConfig

Configures the realtime input behavior in `BidiGenerateContent` .

Fields

`automatic_activity_detection`

`  AutomaticActivityDetection  `

Optional. If not set, automatic activity detection is enabled by default. If automatic voice detection is disabled, the client must send activity signals.

`activity_handling`

`  ActivityHandling  `

Optional. Defines what effect activity has.

`turn_coverage`

`  TurnCoverage  `

Optional. Defines which input is included in the user's turn.

## ActivityHandling

The different ways of handling user activity.

Enums

`ACTIVITY_HANDLING_UNSPECIFIED`

If unspecified, the default behavior is `START_OF_ACTIVITY_INTERRUPTS` .

`START_OF_ACTIVITY_INTERRUPTS`

If true, start of activity will interrupt the model's response (also called "barge in"). The model's current response will be cut-off in the moment of the interruption. This is the default behavior.

`NO_INTERRUPTION`

The model's response will not be interrupted.

## AutomaticActivityDetection

Configures automatic detection of activity.

Fields

`start_of_speech_sensitivity`

`  StartSensitivity  `

Optional. Determines how likely speech is to be detected.

`end_of_speech_sensitivity`

`  EndSensitivity  `

Optional. Determines how likely detected speech is ended.

`prefix_padding_ms`

`int32`

Optional. The required duration of detected speech before start-of-speech is committed. The lower this value the more sensitive the start-of-speech detection is and the shorter speech can be recognized. However, this also increases the probability of false positives.

`silence_duration_ms`

`int32`

Optional. The required duration of detected silence (or non-speech) before end-of-speech is committed. The larger this value, the longer speech gaps can be without interrupting the user's activity but this will increase the model's latency.

`disabled`

`bool`

Optional. If enabled, detected voice and text input count as activity. If disabled, the client must send activity signals.

## EndSensitivity

End of speech sensitivity.

Enums

`END_SENSITIVITY_UNSPECIFIED`

The default is END\_SENSITIVITY\_LOW.

`END_SENSITIVITY_HIGH`

Automatic detection ends speech more often.

`END_SENSITIVITY_LOW`

Automatic detection ends speech less often.

## StartSensitivity

Start of speech sensitivity.

Enums

`START_SENSITIVITY_UNSPECIFIED`

The default is START\_SENSITIVITY\_LOW.

`START_SENSITIVITY_HIGH`

Automatic detection will detect the start of speech more often.

`START_SENSITIVITY_LOW`

Automatic detection will detect the start of speech less often.

## TurnCoverage

Options about which input is included in the user's turn.

Enums

`TURN_COVERAGE_UNSPECIFIED`

If unspecified, the default behavior is `TURN_INCLUDES_ALL_INPUT` .

`TURN_INCLUDES_ONLY_ACTIVITY`

The users turn only includes activity since the last turn, excluding inactivity (e.g. silence on the audio stream).

`TURN_INCLUDES_ALL_INPUT`

The users turn includes all realtime input since the last turn, including inactivity (e.g. silence on the audio stream). This is the default behavior.

### UsageMetadata

Metadata on the usage of the cached content.

Fields

`total_token_count`

`int32`

Total number of tokens that the cached content consumes.

`text_count`

`int32`

Number of text characters.

`image_count`

`int32`

Number of images.

`video_duration_seconds`

`int32`

Duration of video in seconds.

`audio_duration_seconds`

`int32`

Duration of audio in seconds.

### GoAway

Server will not be able to service client soon.

Fields

`time_left`

`  Duration  `

The remaining time before the connection will be terminated as ABORTED. The minimal time returned here is specified differently together with the rate limits for a given model.

### SessionResumptionUpdate

Update of the session resumption state.

Only sent if `BidiGenerateContentSetup.session_resumption` was set.

Fields

`new_handle`

`string`

New handle that represents state that can be resumed. Empty if `resumable` =false.

`resumable`

`bool`

True if session can be resumed at this point.

It might be not possible to resume session at some points. In that case we send update empty new\_handle and resumable=false. Example of such case could be model executing function calls or just generating. Resuming session (using previous session token) in such state will result in some data loss.

`last_consumed_client_message_index`

`int64`

Index of last message sent by client that is included in state represented by this SessionResumptionToken. Only sent when `SessionResumptionConfig.transparent` is set.

Presence of this index allows users to transparently reconnect and avoid issue of losing some part of realtime audio input/video. If client wishes to temporarily disconnect (for example as result of receiving GoAway) they can do it without losing state by buffering messages sent since last `SessionResmumptionTokenUpdate` . This field will enable them to limit buffering (avoid keeping all requests in RAM).

It will not be used for 'resumption to restore state' some time later -- in those cases partial audio and video frames are likely not needed.

## What's next

  - Learn more about [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .
  - For examples, see the [Function calling reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/function-calling) .
