---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral
title: Mistral AI models
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

Mistral AI models on Gemini Enterprise Agent Platform offer fully managed and serverless models as APIs. To use a Mistral AI model on Agent Platform, send a request directly to the Agent Platform API endpoint. Because Mistral AI models use a managed API, there's no need to provision or manage infrastructure.

You can stream your responses to reduce the end-user latency perception. A streamed response uses server-sent events (SSE) to incrementally stream the response.

You pay for Mistral AI models as you use them (pay as you go). For pay-as-you-go pricing, see Mistral AI model pricing on the Gemini Enterprise Agent Platform [pricing page](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing#partner-models) .

> To see an example of getting started with Mistral AI models on Agent Platform, run the "Getting Started with Mistral AI Models" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/mistralai_intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fmistralai_intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fvertex-ai-samples%2Fmain%2Fnotebooks%2Fofficial%2Fgenerative_ai%2Fmistralai_intro.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/vertex-ai-samples/blob/main/notebooks/official/generative_ai/mistralai_intro.ipynb)

## Available Mistral AI models

The following models are available from Mistral AI to use in Gemini Enterprise Agent Platform. To access a Mistral AI model, go to its Model Garden model card.

metro [Mistral Medium 3](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/mistral-medium-3) A versatile multimodal model designed for advanced reasoning, programming, long-context document understanding, single-node high throughput, and agentic workflows.

metro [Mistral OCR (25.05)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/mistral-ocr) Optical Character Recognition API for rich document understanding, extracting interleaved imagery, tables, graphs, and LaTeX formatting for multimodal RAG pipelines.

metro [Mistral Small 3.1 (25.03)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/mistral-small-3-1) A versatile, low-latency multimodal model with a 128,000 token context window, optimized for high-efficiency chat, programming, and instruction following.

metro [Codestral 2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral/codestral-2) Specialized code generation model built for high-precision fill-in-the-middle (FIM) completion, code review, refactoring, and developer tooling.

## Use Mistral AI models

You can use curl commands to send requests to the Gemini Enterprise Agent Platform endpoint using the following model names:

  - For Mistral Medium 3, use `mistral-medium-3`
  - For Mistral OCR (25.05), use `mistral-ocr-2505`
  - For Mistral Small 3.1 (25.03), use `mistral-small-2503`
  - For Codestral 2, use `codestral-2`

For more information about using the Mistral AI SDK, see the [Mistral AI Gemini Enterprise Agent Platform documentation](https://docs.mistral.ai/deployment/cloud/vertex/) .

### Before you begin

To use Mistral AI models with Gemini Enterprise Agent Platform, you must perform the following steps. The Agent Platform API ( `aiplatform.googleapis.com` ) must be enabled to use Gemini Enterprise Agent Platform. If you already have an existing project with the Agent Platform API enabled, you can use that project instead of creating a new project.

1.  Go to one of the following Model Garden model cards, then click **Enable** :
      - 
      - 
      - 
      - 
#### Make a streaming call to a Mistral AI model

The following sample makes a streaming call to a Mistral AI model.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION : A region that supports Mistral AI models.

  - MODEL : The [model name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral#model-list) you want to use. In the request body, exclude the `@` model version number.

  - ROLE : The role associated with a message. You can specify a `user` or an `assistant` . The first message must use the `user` role. The models operate with alternating `user` and `assistant` turns. If the final message uses the `assistant` role, then the response content continues immediately from the content in that message. You can use this to constrain part of the model's response.

  - STREAM : A boolean that specifies whether the response is streamed or not. Stream your response to reduce the end-use latency perception. Set to `true` to stream the response and `false` to return the response all at once.

  - CONTENT : The content, such as text, of the `user` or `assistant` message.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately 3.5 characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:streamRawPredict

Request JSON body:

    {
    "model": MODEL,
      "messages": [
       {
        "role": "ROLE",
        "content": "CONTENT"
       }],
      "max_tokens": MAX_TOKENS,
      "stream": true
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:streamRawPredict"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:streamRawPredict" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    data: {
        "id": "0e9c8e69e5924f729b39bc60bac9e0be",
        "object": "chat.completion.chunk",
        "created": 1720807292,
        "model": "MODEL",
        "choices": [
            {
                "index": 0,
                "delta": {
                  "content": "OUTPUT"
                },
                "finish_reason": null,
                "logprobs": null
            }
        ]
    }
    
    data: {
        "id": "0e9c8e69e5924f729b39bc60bac9e0be",
        "object": "chat.completion.chunk",
        "created": 1720807292,
        "model": "MODEL",
        "choices": [
            {
                "index": 0,
                "delta": {
                  "content": "OUTPUT"
                },
                "finish_reason": null,
                "logprobs": null
            }
        ]
    }
    ...

#### Make a unary call to a Mistral AI model

The following sample makes a unary call to a Mistral AI model.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - LOCATION : A region that supports Mistral AI models.

  - MODEL : The [model name](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral#model-list) you want to use. In the request body, exclude the `@` model version number.

  - ROLE : The role associated with a message. You can specify a `user` or an `assistant` . The first message must use the `user` role. The models operate with alternating `user` and `assistant` turns. If the final message uses the `assistant` role, then the response content continues immediately from the content in that message. You can use this to constrain part of the model's response.

  - STREAM : A boolean that specifies whether the response is streamed or not. Stream your response to reduce the end-use latency perception. Set to `true` to stream the response and `false` to return the response all at once.

  - CONTENT : The content, such as text, of the `user` or `assistant` message.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately 3.5 characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:rawPredict

Request JSON body:

    {
    "model": MODEL,
      "messages": [
       {
        "role": "ROLE",
        "content": "CONTENT"
       }],
      "max_tokens": MAX_TOKENS,
      "stream": false
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:rawPredict"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/mistralai/models/MODEL:rawPredict" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
        "id": "e71d13ffb77344a08e34e0a22ea84458",
        "object": "chat.completion",
        "created": 1720806624,
        "model": "MODEL",
        "choices": [
            {
                "index": 0,
                "message": {
                    "role": "assistant",
                    "content": "OUTPUT",
                    "tool_calls": null
                },
                "finish_reason": "stop",
                "logprobs": null
            }
        ],
        "usage": {
            "prompt_tokens": 17,
            "total_tokens": 295,
            "completion_tokens": 278
        }
    }

## Mistral AI model region availability and quotas

For Mistral AI models, a quota applies for each region where the model is available. The quota is specified in queries per minute (QPM) and tokens per minute (TPM). TPM includes both input and output tokens.

> **Important:** Machine learning (ML) processing for all available Mistral AI models occurs within the US when requests are made to regionally-available APIs in the US, or within the EU when requests are made to regionally-available APIs in Europe.

Model

Region

Quotas

Context length

Mistral Medium 3

`us-central1`

  - QPM: 90
  - TPM: 315,000

128,000

`europe-west4`

  - QPM: 90
  - TPM: 315,000

128,000

Mistral OCR (25.05)

`us-central1`

  - QPM: 30
  - Pages per request: 30 (1 page = 1 million input tokens and 1 million output tokens)

30 pages

`europe-west4`

  - QPM: 30
  - Pages per request: 30 (1 page = 1 million input tokens and 1 million output tokens)

30 pages

Mistral Small 3.1 (25.03)

`us-central1`

  - QPM: 60
  - TPM: 200,000

128,000

`europe-west4`

  - QPM: 60
  - TPM: 200,000

128,000

Codestral 2

`us-central1`

  - QPM: 1,100
  - Input TPM: 1,100,000
  - Output TPM: 110,000

128,000 tokens

`europe-west4`

  - QPM: 1,100
  - Input TPM: 1,100,000
  - Output TPM: 110,000

128,000 tokens

If you want to increase any of your quotas for Agent Platform, you can use the Google Cloud console to request a quota increase. To learn more about quotas, see the [Cloud Quotas overview](https://docs.cloud.google.com/docs/quotas/overview) .
