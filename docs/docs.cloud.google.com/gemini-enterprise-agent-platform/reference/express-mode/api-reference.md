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

Gemini Enterprise Agent Platform in express mode lets you try a subset of Gemini Enterprise Agent Platform features by using only an express mode API key. This page shows you the REST resources available for Gemini Enterprise Agent Platform in express mode.

Unlike the standard REST resource endpoints on Google Cloud, endpoints that are available when using Gemini Enterprise Agent Platform in express mode use the global endpoint `aiplatform.googleapis.com` and don't include `projects` or `locations` . For example, the following shows the difference between standard and express mode endpoints for the datasets resource:

**Standard Gemini Enterprise Agent Platform endpoint format** : `https://{location}-aiplatform.googleapis.com/v1/projects/{project}/locations/{location}/{model}:generateContent`

**Endpoint format for Gemini Enterprise Agent Platform in express mode** : `https://aiplatform.googleapis.com/v1/{model}:generateContent`

## REST Resource: [v1.publishers.models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1/publishers.models)

Methods

`  countTokens  `

`POST /v1/{endpoint}:countTokens`  
Perform a token counting.

`  generateContent  `

`POST /v1/{model}:generateContent`  
Generate content with multimodal inputs.

`  streamGenerateContent  `

`POST /v1/{model}:streamGenerateContent`  
Generate content with multimodal inputs with streaming support.

## REST Resource: [v1beta1.publishers.models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/express-mode/rest/v1beta1/publishers.models)

Methods

`  countTokens  `

`POST /v1beta1/{endpoint}:countTokens`  
Perform a token counting.

`  generateContent  `

`POST /v1beta1/{model}:generateContent`  
Generate content with multimodal inputs.

`  streamGenerateContent  `

`POST /v1beta1/{model}:streamGenerateContent`  
Generate content with multimodal inputs with streaming support.
