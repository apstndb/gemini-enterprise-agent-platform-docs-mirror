---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/api-reference
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/api-reference
title: Gemini Enterprise Agent Platform in express mode REST API reference
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Gemini Enterprise Agent Platform in express mode lets you try a subset of Agent Platform features by using an express mode API key passed in the `x-goog-api-key` HTTP header (or the `key` query parameter). This document shows the REST resources available for Agent Platform in express mode.

Unlike the standard REST resource endpoints on Google Cloud, endpoints that are available when using Agent Platform in express mode use the global endpoint `aiplatform.googleapis.com` and don't include `projects` or `locations` . In the following REST resource paths, `{model}` uses the resource path format `publishers/google/models/ `` MODEL_ID` :

- **Standard Agent Platform endpoint format** : `https:// `` LOCATION `` -aiplatform.googleapis.com/v1/projects/ `` PROJECT_ID `` /locations/ `` LOCATION `` /publishers/google/models/ `` MODEL_ID `` :generateContent`
- **Endpoint format for Agent Platform in express mode** : `https://aiplatform.googleapis.com/v1/publishers/google/models/ `` MODEL_ID `` :generateContent`

## REST Resource: [v1.publishers.models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models)

| Methods                                                                                                                                                          |                                                                                                          |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| [`countTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models/countTokens)                     | `POST /v1/{endpoint}:countTokens` Perform a token counting.                                              |
| [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models/generateContent)             | `POST /v1/{model}:generateContent` Generate content with multimodal inputs.                              |
| [`streamGenerateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models/streamGenerateContent) | `POST /v1/{model}:streamGenerateContent` Generate content with multimodal inputs with streaming support. |

## REST Resource: [v1beta1.publishers.models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1beta1/publishers.models)

| Methods                                                                                                                                                               |                                                                                                               |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| [`countTokens`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1beta1/publishers.models/countTokens)                     | `POST /v1beta1/{endpoint}:countTokens` Perform a token counting.                                              |
| [`generateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1beta1/publishers.models/generateContent)             | `POST /v1beta1/{model}:generateContent` Generate content with multimodal inputs.                              |
| [`streamGenerateContent`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1beta1/publishers.models/streamGenerateContent) | `POST /v1beta1/{model}:streamGenerateContent` Generate content with multimodal inputs with streaming support. |
