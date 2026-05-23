---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/troubleshooting
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/troubleshooting
title: Troubleshooting Gemini Live API
description: Learn how to troubleshoot common issues with Gemini Live API.
data_source: docs.cloud.google.com
---

This document provides troubleshooting steps for issues that you might encounter when using Gemini Live API.

## Connection drops unexpectedly

If your session connection drops unexpectedly, it might be due to token limits, session connection timeouts, or network issues.

### Behavior

Session disconnected with error code `1000` or `1006` .

### Possible reasons

  - Context window compression isn't enabled and context token exceeds the session's context token limit (up to 128k).
  - No session resumption logic is implemented or resumption logic isn't correctly implemented.
  - Unstable internet connection.

### Reasons and solutions

  - **Tokens exceed the session's context token limit:** To prevent exceeding the session's context token limit, activate context compression. This might impact the quality of the conversation, as the model will intermittently discard earlier parts of the chat history.

  - **Session connection expires after 10 minutes:** Manage session resumption to allow for longer interactions. For further details, consult the best practices for session resumption.

  - **Unstable internet connection:** Verify the condition of your internet connection, as fluctuations in stability may result in connectivity problems.

## Model failed to understand the user

If the model doesn't seem to understand your input, ensure your audio is formatted correctly and consider your microphone quality and background noise.

### Behavior

The model responds with irrelevant information, responds with incorrect information, or asks the user to repeat.

### Possible reasons

  - Input audio format isn't correct.
  - Microphone quality isn't good.
  - The background noise is too high.

### Reasons and solutions

  - **Input audio format isn't correct:** Verify that the input audio uses a little-endian, 16-bit PCM format with a 16 kHz sampling rate and a single mono channel.

  - **Microphone quality isn't good:** Test the microphone quality by recording a short audio and playing it back. If the microphone quality isn't good, try to use a microphone with better quality.

  - **Background noise is too high:** Test the background noise level by recording a short audio and playing it back. If the background noise level is too high, try to move the microphone closer to the user or use a microphone with better noise cancellation.

## Model isn't responding

If you aren't receiving a response from the model, check your voice activity detection options and WebSocket connection.

### Behavior

No response from the model.

### Possible reasons

  - VAD settings aren't correctly set.
  - WebSocket connection got interrupted.

### Reasons and solutions

  - **VAD set incorrectly:** VAD is disabled by the user. In this case, the model will keep waiting for the user's speech and won't respond to the user. Make sure to send `ActivityStart` and `ActivityEnd` events to the model if the VAD is disabled.

  - **WebSocket connection got interrupted:** If the WebSocket connection is interrupted, there will be no communication between the client and the server. Check the WebSocket connection status and make sure it is properly established.

## Cannot interrupt the model

If you're unable to interrupt the model while it's speaking, ensure you're handling the playback buffer and streaming audio correctly.

### Behavior

The model continues to speak without interruption from the user.

### Possible reasons

  - Failed to flush playback buffer.
  - Failed to stream audio to Gemini Live API.
  - Customized VAD isn't correctly implemented.

### Reasons and solutions

  - **Failed to flush playback buffer:** The client should flush the playback buffer immediately when receiving an interrupt signal from the model. Otherwise, the model will keep talking.

  - **Failed to stream audio to Gemini Live API:** The client should stream audio to Gemini Live API in chunks between 20 ms and 40 ms to minimize latency. If the client fails to stream audio to Gemini Live API, the model won't send an interrupt signal to the client.

  - **Customized VAD isn't correctly implemented:** If the customized VAD fails to recognize the start of speech or the client fails to send `ActivityStart` signal to the model, the model won't send an interrupt signal to the client.
