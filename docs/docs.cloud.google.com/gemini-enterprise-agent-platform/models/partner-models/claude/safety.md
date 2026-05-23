---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/safety
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/safety
title: Safety classifiers for Claude in Gemini Enterprise Agent Platform
description: description
data_source: docs.cloud.google.com
---

Gemini Enterprise Agent Platform includes a safety classifier that filters requests to all hosted Anthropic models that may contain images that include Child Sexual Abuse Material (CSAM). Gemini Enterprise Agent Platform's suspected CSAM safety classifier is separate from the Trust and Safety (T\&S) filters shipped directly with Anthropic's models.

This document covers which parts of the request and response that the suspected CSAM safety classifier filters and what happens when the classifier blocks a request.

Safety and content filters act as a barrier to prevent harmful output, but they don't directly influence the model's behavior. To learn more about model steerability, see [System instructions for safety](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/safety-system-instructions) .

## Unsafe prompts

The suspected CSAM classifier filters only the images in requests to Anthropic models in Gemini Enterprise Agent Platform. The suspected CSAM classifier doesn't filter the model's outputs.

Requests that trigger the suspected CSAM classifier are blocked and return a `200` HTTP status code with the following message:

    {
      "promptFeedback": {
        "blockReason": "PROHIBTED_CONTENT"
      }
    }

If the request is blocked by the classifier, the request stream is cancelled and the following message is returned:

    "event": "vertex-block-event",
    "data": {"promptFeedback": {"blockReason": "PROHIBITED_CONTENT"}}

## Location availability

The suspected CSAM classifier is available in all [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#quotas) .
