---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/demos
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/live-api/demos
title: Demo apps and resources for using the Gemini Live API
description: Explore demo applications and resources for using the Gemini Gemini Live API on Gemini Enterprise Agent Platform, including web apps, ADK guides, and tools.
data_source: docs.cloud.google.com
---

This page provides a collection of reference implementations for the Gemini Live API on Gemini Enterprise Agent Platform. Ranging from dependency-free JavaScript starters to comprehensive React-based architectures, these demos demonstrate how to build robust, real-time voice agents using the Gemini Live API and ADK.

## Demo apps

  - [React demo app](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/native-audio-websocket-demo-apps/react-demo-app) : A comprehensive React client featuring real-time streaming, tool use, and media handling.
  - [Plain JS demo app](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/native-audio-websocket-demo-apps/plain-js-demo-app) : A dependency-free JavaScript implementation for understanding core API mechanics.
  - [Real-time advisor](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/native-audio-websocket-demo-apps/realtime-advisor-demo-app) : A specialized advisor persona that can switch between silent and outspoken modes.
  - [Customer support agent](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/native-audio-websocket-demo-apps/customer-support-demo-app) : An advanced agent with emotion detection, multimodal input, and tool execution.
  - [Gaming assistant](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/native-audio-websocket-demo-apps/gaming-assistant-demo-app) : A gaming companion with persona switching and screen sharing capabilities.
  - [Gemini Live Telephony App](https://github.com/GoogleCloudPlatform/generative-ai/tree/main/gemini/sample-apps/gemini-live-telephony-app) : A real-time, voice-to-AI application that uses Twilio for telephony, a FastAPI backend, and the Gemini Live API for conversational AI.

## ADK bidi-streaming development guide

The [Agent Development Kit](https://google.github.io/adk-docs/) (ADK) provides a production-ready framework for building Bidi-streaming applications with the Live API. The following guide and demos introduce ADK's streaming architecture, which enables real-time, two-way communication between users and AI agents through multimodal channels (text, audio, video).

  - [ADK Bidi-streaming development guide series](https://google.github.io/adk-docs/streaming/dev-guide/part1/)
  - [Bidi-streaming demo](https://github.com/google/adk-samples/tree/main/python/agents/bidi-demo)

## Other tools

  - [PCM audio debugger](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/multimodal-live-api/pcm-audio-debugger) : A standalone tool for testing and debugging raw PCM audio streams and WebSocket connections.
