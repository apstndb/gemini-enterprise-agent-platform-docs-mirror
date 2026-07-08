---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens
title: Count tokens for Claude models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

The `count-tokens` endpoint lets you determine the number of tokens in a message before sending it to Claude, helping you make informed decisions about your prompts and usage.

There is no cost for using the `count-tokens` endpoint.

## Supported Claude models

The following models support count tokens:

  - [Claude Sonnet 5 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-5)
  - [Claude Fable 5 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-fable-5)
  - [Claude Opus 4.8 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-8)
  - [Claude Opus 4.7 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-7)
  - [Claude Opus 4.6 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-6)
  - [Claude Sonnet 4.6 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-6)
  - [Claude Opus 4.5 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-5)
  - [Claude Opus 4.1 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4-1)
  - [Claude Opus 4 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-opus-4)
  - [Claude Sonnet 4.5 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4-5)
  - [Claude Sonnet 4 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-sonnet-4)
  - [Claude Haiku 4.5 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-haiku-4-5)
  - [Claude 3.5 Haiku on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-3-5-haiku)

## Supported regions

The following regions support count tokens:

  - `us-east5`
  - `europe-west1`
  - `asia-southeast1`

## Count tokens in basic messages

To count tokens, send a `rawPredict` request to the `count-tokens` endpoint. The body of the request must contain the model ID of the model you want to count tokens against.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : A [region](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens#regions) that supports Anthropic Claude models. To use the global endpoint, see [Specify the global endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models#global) .
  - MODEL : The [model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/count-tokens#model-list) to count tokens against.
  - ROLE : The role associated with a message. You can specify a `user` or an `assistant` . The first message must use the `user` role. Claude models operate with alternating `user` and `assistant` turns. If the final message uses the `assistant` role, then the response content continues immediately from the content in that message. You can use this to constrain part of the model's response.
  - CONTENT : The content, such as text, of the `user` or `assistant` message.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/count-tokens:rawPredict

Request JSON body:

    {
      "model": "MODEL",
      "messages": [
        {
          "role": "user",
          "content":"how many tokens are in this request?"
        }
      ],
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/count-tokens:rawPredict"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/anthropic/models/count-tokens:rawPredict" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    { "input_tokens": 14 }

For information on how to count tokens in messages with tools, images, and PDFs, see [Anthropic's documentation](https://docs.anthropic.com/en/docs/build-with-claude/token-counting) .

## Quotas

By default, the quota for the `count-tokens` endpoint is 2000 requests per minute.
