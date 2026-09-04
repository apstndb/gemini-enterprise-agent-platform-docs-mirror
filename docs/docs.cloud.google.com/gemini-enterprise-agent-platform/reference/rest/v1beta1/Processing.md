---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Processing
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/Processing
title: Processing
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

How the model processes input media for understanding.

Enums

`PROCESSING_UNSPECIFIED`

Default. uses model-specific processing (3.5 Pro+ --\> AGENTIC, older models --\> STATIC)

`STATIC`

Fixed-rate frame extraction. All frames placed in context.

`AGENTIC`

Model-driven dynamic navigation.
