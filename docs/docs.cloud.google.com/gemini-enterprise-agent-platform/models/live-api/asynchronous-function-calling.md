---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling
title: Asynchronous function calling with Gemini Live API
description: Learn how to use asynchronous function calling in Gemini Live API to execute functions in parallel with conversation, manage background processing, and handle function responses using policies like SILENT, WHEN_IDLE, and INTERRUPT.
data_source: docs.cloud.google.com
---

> **Caution:** `gemini-live-2.5-flash-preview-native-audio-09-2025` will be deprecated and removed on March 19, 2026. Migrate any workflows to `gemini-live-2.5-flash-native-audio` .

When building real-time voice agents, some function calls can block the model's execution, which causes the audio stream to go quiet and the user to be left waiting in silence. With Gemini Live API, all function calls are non-blocking by default, which lets you [execute functions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) in parallel with the main conversation flow. This process is called *asynchronous function calling* . Your backend can process heavy tasks like searching live flight prices or querying complex external APIs in the background, while the model continues to listen, speak, and converse naturally with the user. Gemini Live API lets function calls process in the background without interrupting the user's interaction with the model, enabling more fluid and real-time interactions.

Asynchronous function calling lets you complete tasks like booking appointments, setting reminders, or fetching data without pausing the conversation. For example, a user can request to book a flight and immediately ask for weather information while the booking is processed in the background.

> To learn more, run the "Asynchronous Function Calling" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_async_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_async_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fmultimodal-live-api%2Fintro_async_function_calling.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/intro_async_function_calling.ipynb)

## Example of asynchronous function calling

This example demonstrates a user booking a flight and asking for the time in New York while the `book_ticket` function runs asynchronously in the background:

    User: Please book the 2:00 PM flight to New York for me.
    
    Model: function_call: {name: "book_ticket"}
    //(The "book_ticket" function call is sent to the client.)
    //(Right after the "book_ticket" function call is received, the client sends a text message to the model: "repeat this sentence 'I'm booking your ticket now, please wait.'")
    //(The client runs the function call asynchronously in the background.)
    Model: I'm booking your ticket now, please wait.
    
    User: What is the current time in New York?
    
    Model: The current time in New York is 12:00pm.
    
    //(Once the book_ticket function finishes, the client sends the result.)
    Function_response: {name: "book_ticket", response: {booking_status: "booked"}}
    
    Model: Your flight has been booked. Expect a confirmation text on your phone within 5 minutes.

## Implement asynchronous function calling

This section provides a series of examples using the Python version of the Agent Platform SDK to build a highly responsive, concurrent architecture that uses Gemini Live API's asynchronous function calling capability. The examples are broken down into the following tasks:

  - [Define your tools](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#define-tools)
  - [Handle function calls from the message stream](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#handle-function-calls)
  - [Manage user expectations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#manage-expectations)

### Define your tools

Asynchronous function calling is enabled at the model level, so you can specify what tools you want to use in the request configuration like you would for any standard Gemini API call. This allows the model to continue conversing while your tool executes:

    from google import genai
    from google.genai import types
    
    # 1. A tool that takes a long time to execute
    search_live_flights = {
        "name": "search_live_flights",
        "description": "Searches airlines for current flight prices. Can take up to 10 seconds."
    }
    
    # 2. A tool that executes instantly
    get_current_weather = {
        "name": "get_current_weather",
        "description": "Gets the current weather for a given city."
    }
    
    tools = [{"function_declarations": [search_live_flights, get_current_weather]}]

### Handle function calls from the message stream

When one or more functions should be called by the model, Gemini Live API sends a `tool_call` event through the real-time message stream.

Your backend must not block the stream because the model expects to keep running. When you receive a call for a slow function (like `search_live_flights` ), you must pass it to a background worker. If you use an `await` directly in your main message loop for a 10-second task, you will freeze the connection. Fast tasks (like `get_current_weather` ) can be safely awaited.

    import asyncio
    
    async def handle_stream(session):
        async for response in session.receive():
            # Check if the model is asking to use a tool
            if response.tool_call is not None:
                for fc in response.tool_call.function_calls:
    
                    if fc.name == "search_live_flights":
                        # Pass to a background task so we don't block the receive loop!
                        asyncio.create_task(background_flight_search(fc.id, fc.args, session))
    
                    elif fc.name == "get_current_weather":
                        # Instant lookups can be safely awaited directly
                        await instant_weather_lookup(fc.id, fc.args, session)

### Manage user expectations

To manage expectations during long-running asynchronous function calls, it's recommended that the client initiate a text message. This message should prompt the system to inform the user that the request is being processed and request their patience. For example, after a function call is received by the client, the client can send a text message to the model such as: "repeat this sentence: 'I'm booking your ticket now, please wait.'".

The following example dialog shows this exchange:

    User: Please book the 2:00 PM flight to New York for me.
    Model: function_call: {name: "book_ticket"}
    //(The "book_ticket" function call is sent to the client.)
    //(Right after the "book_ticket" function call is received, the client sends a text message to the model: "repeat this sentence 'I'm booking your ticket now, please wait.'")
    //(The client runs the function call asynchronously in the background.)
    Model: I'm booking your ticket now, please wait.
    User: What is the current time in New York?
    Model: The current time in New York is 12:00pm.
    //(Once the "book_ticket" function call finishes, the client sends in the response.)
    Function_response: {name: "book_ticket", response: {booking_status: "booked"}}
    Model: Your flight has been booked. Expect a confirmation text on your phone within 5 minutes.

This proactive messaging strategy has the following benefits:

  - Informs the user of current system operations, which manages expectations during long-running function calls.
  - Reduces the frequency of redundant short user prompts, such as " *hello?* " or " *are you there?* ". These often occur during long periods of system silence while asynchronous function calls are being processed. This can minimize the risk of duplicated function calls triggered by these repeated user inquiries.
  - Providing an extra system prompt can lower the probability of creating duplicate calls in subsequent interactions.

## Handle duplicate function calls

There is a small chance that the model generates duplicated function calls before receiving a response for the first call. If your use case allows it, your application can ignore duplicate function calls if a response for the same function call is still pending.

The following example shows how a client can ignore a duplicate function call:

    User: Please book the 2:00 PM flight to New York for me.
    
    Model: function_call: {name: "book_ticket"}
    //(The "book_ticket" function call is sent to the client. It is running asynchronously in the background.)
    
    User: What is the current time in New York?
    Model: The current time in New York is 12:00pm. + function_call: {name: "book_ticket"}
    //(The duplicated "book_ticket" can be ignored by the client since the response for the first "book_ticket" has not been sent to the model yet.)
    
    //(The first "book_ticket" function call finishes, and client sends in the response.)
    Function_response: {name: "book_ticket", response: {booking_status: "booked"}}
    
    Model: Your flight has been booked. Expect a confirmation text on your phone within 5 minutes.

## Handle asynchronous function responses

When an asynchronous function call is complete, your application sends the result to the model in a `function_response` . While your backend is processing a function call, like searching for flights, the user might ask the model a completely different question, such as, " *What's the weather like in London?* ". The model will respond to the request in real-time, in parallel with the function call execution. As the user might be in an ongoing interaction with the model when function execution completes, you can specify a policy that defines how the model should handle this incoming response. You can specify one of the following policies:

  - [`SILENT`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#silent-policy)
  - [`WHEN_IDLE`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#when-idle-policy)
  - [`INTERRUPT`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/asynchronous-function-calling#interrupt-policy)

To specify a policy, include the `scheduling` field in your `function_response` payload:

    {
      "name": "book_ticket",
      "scheduling": "WHEN_IDLE",
      "response": {
        "booking_status": "booked"
      }
    }

If you omit the `scheduling` field, Gemini Live API uses its original method for handling function responses for backward compatibility.

The following Python example shows how to format and send a `function_response` with `scheduling="WHEN_IDLE"` to wait for a natural pause in conversation before announcing results:

    aearcync def background_flight_search(call_id, args, session):
        # 1. Simulate a slow API call taking 5 seconds
        await asyncio.sleep(5)
        flight_data = ["Air Canada AC758: $350", "WestJet WS12: $290"]
    
        # 2. Format the response
        function_response = types.FunctionResponse(
            id=call_id,
            name="search_live_flights",
            response={ "status": "success", "flights": flight_data },
            scheduling="WHEN_IDLE" # Wait for a moment to tell the user
        )
    
        # 3. Send it back into the live session
        await session.send_tool_response(function_responses=[function_response])

The following policies can be specified in the `scheduling` field for managing function responses:

### SILENT response policy

With the `SILENT` policy, the function response is added to the model's context, but the model doesn't generate a response for it, and any ongoing user interaction is not interrupted.

    User: Please book the 2:00 PM flight to New York for me.
    
    Model: function_call: {name: "book_ticket"}
    //(The book_ticket function call is sent to the client and starts running asynchronously in the background.)
    
    User: What is the current time in New York?
    Model: The current time in New York is 12:00pm.
    
    //(The book_ticket function finishes, and client sends the result with scheduling: "SILENT".)
    Function_response: {name: "book_ticket", scheduling: "SILENT", response: {booking_status: "booked"}}
    //(The model doesn't generate a response for the function response.)
    
    User: Is my flight ticket booked?
    Model: Yes. Your flight has been booked.

### WHEN\_IDLE response policy

With the `WHEN_IDLE` policy, the model generates a response to the function response only when there is no active user interaction. If a user interaction is in progress, the model waits for it to complete before generating a response to avoid interruption.

    User: Please book the 2:00 PM flight to New York for me.
    
    Model: function_call: {name: "book_ticket"}
    //(The book_ticket function call is sent to the client and starts running asynchronously in the background.)
    
    User: What is the current time in New York?
    
    //(The book_ticket function finishes, and client sends the result with scheduling: "WHEN_IDLE".)
    Function_response: {name: "book_ticket", scheduling: "WHEN_IDLE", response: {booking_status: "booked"}}
    //(The ongoing interaction about the time is not interrupted.)
    
    Model: The current time in New York is 12:00pm.
    //(After responding to the user's time query, the model issues the response for the book_ticket function.)
    Model: Your flight has been booked. Expect a confirmation text on your phone within 5 minutes.

### INTERRUPT response policy

With the `INTERRUPT` policy, the model generates a response to the function response immediately, interrupting any ongoing user interaction.

    User: Please book the 2:00 PM flight to New York for me.
    
    Model: function_call: {name: "book_ticket"}
    //(The book_ticket function call is sent to the client and starts running asynchronously in the background.)
    
    User: What is the current time in New York?
    
    //(The book_ticket function finishes, and client sends the result with scheduling: "INTERRUPT".)
    Function_response: {name: "book_ticket", scheduling: "INTERRUPT", response: {booking_status: "booked"}}
    //(The ongoing interaction about the time is interrupted, and model skips responding to it.)
    
    Model: Your flight has been booked. Expect a confirmation text on your phone within 5 minutes.

## Best practices

  - **Design for concurrency** : Always offload slow tools (like querying external APIs or running RAG pipelines) to background tasks in your backend. Let the model keep handling the active audio stream.
  - **Avoid INTERRUPT unless necessary** : Use `INTERRUPT` for critical alerts. For background tasks, `SILENT` or `WHEN_IDLE` provides a much smoother, polite user experience.
  - **Independent chat turns** : In Gemini Live API, tool execution is completely independent of chat turns. The conversation can branch, continue, and flow naturally while your tool processes in the background.
  - **The "Silent" caveat** : The model may still occasionally try to verbally narrate a tool's execution even if scheduled as `SILENT` . To enforce true silence, add explicit guardrails to your System Instructions (for example, "When using \[Tool Name\], perform a SILENT EXECUTION and say nothing"), or use a "fire-and-forget" backend pattern where you don't send a `FunctionResponse` back to the model at all.

## What's next

Overview

### [Live API overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api)

Get an overview of Live API.

Reference

### [Live API reference guide](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/model-reference/multimodal-live)

Reference guide for Live API.

Guide

### [Start and manage live sessions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/start-manage-session)

Learn how to start and manage live sessions with Live API.

Guide

### [Configure Gemini capabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/configure-gemini-capabilities)

Learn how to configure Gemini capabilities for Live API.
