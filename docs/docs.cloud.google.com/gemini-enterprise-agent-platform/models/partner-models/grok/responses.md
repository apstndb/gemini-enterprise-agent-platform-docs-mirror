---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/responses
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/responses
title: Call Responses API
description: Call XAI Grok models using the Responses API. Implement requests to generate responses.
data_source: docs.cloud.google.com
---

XAI's Grok models on Gemini Enterprise Agent Platform support the [Responses API](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/reference/rest/v1beta1/projects.locations.endpoints.openapi/responses) for generating responses.

This page shows how to make calls to Grok models using the Responses API.

## Before you begin

To use Grok models with Gemini Enterprise Agent Platform, you must perform the following steps. The Gemini Enterprise Agent Platform API ( `aiplatform.googleapis.com` ) must be enabled.

## Make a stateless call to the Responses API

To use stateless functionalities, explicitly set `store` to `false` (or `False` in Python) in your requests. The default value for `store` is `true` .

### Make a non-streaming call to the Responses API

The following samples show how to make a non-streaming call to the Responses API:

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    from openai import OpenAI
    client = OpenAI()
    response = client.responses.create(
        model="MODEL",
        input="INPUT",
        max_output_tokens=MAX_OUTPUT_TOKENS,
        stream=False,
        store=False,
    )
    print(response)

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

  - INPUT : The prompt or input for the model.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

  - INPUT : The prompt or input for the model.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses

Request JSON body:

    {
      "model": "MODEL",
      "input": "INPUT",
      "max_output_tokens": MAX_OUTPUT_TOKENS,
      "stream": false,
      "store": false
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"

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
        -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content

The following example shows a complete curl request:

    curl -s -X POST \
      -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
      -d '{
        "model": "xai/grok-4.20-reasoning",
        "input": "Explain black holes in one short sentence.",
        "max_output_tokens": 100,
        "stream": false,
        "store": false
      }'

Based on the Responses API definition, a non-streaming response will contain a unique ID, model metadata, usage statistics, and an output array containing the generated text.

    {
      "background": false,
      "completed_at": 1778892918,
      "created_at": 1778892916,
      "error": null,
      "frequency_penalty": 0,
      "id": "c8AHavnIMP6UifEPgIfcgAg",
      "incomplete_details": null,
      "instructions": null,
      "max_output_tokens": null,
      "max_tool_calls": null,
      "metadata": {
        "system_fingerprint": "fp_39c5j0a3e9"
      },
      "model": "MODEL",
      "object": "response",
      "output": [
        {
          "content": [
            {
              "annotations": [],
              "logprobs": [],
              "text": "OUTPUT_TEXT",
              "type": "output_text"
            }
          ],
          "id": "msg_c8AHavnIMP6UifEPgIfcgAg",
          "role": "assistant",
          "status": "completed",
          "type": "message"
        }
      ],
      "parallel_tool_calls": true,
      "presence_penalty": 0,
      "previous_response_id": null,
      "prompt_cache_key": null,
      "reasoning": {
        "effort": "medium",
        "summary": "detailed"
      },
      "safety_identifier": null,
      "service_tier": "default",
      "status": "completed",
      "store": false,
      "temperature": 0.7,
      "text": {
        "format": {
          "type": "text"
        }
      },
      "tool_choice": "auto",
      "tools": [],
      "top_logprobs": 0,
      "top_p": 0.95,
      "truncation": "disabled",
      "usage": {
        "extra_properties": {
          "google": {
            "traffic_type": "ON_DEMAND"
          }
        },
        "input_tokens": 335,
        "input_tokens_details": {
          "cached_tokens": 320
        },
        "num_server_side_tools_used": 0,
        "num_sources_used": 0,
        "output_tokens": 305,
        "output_tokens_details": {
          "reasoning_tokens": 284
        },
        "total_tokens": 640
      },
      "user": null
    }

### Make a streaming call to the Responses API

The following samples show how to make a streaming call to the Responses API:

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    from openai import OpenAI
    client = OpenAI()
    stream = client.responses.create(
        model="MODEL",
        input="INPUT",
        max_output_tokens=MAX_OUTPUT_TOKENS,
        stream=True,
        store=False,
    )
    for event in stream:
        if event.type == "response.output_text.delta":
            print(event.delta, end="")

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

  - INPUT : The prompt or input for the model.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

  - INPUT : The prompt or input for the model.

  - MAX\_OUTPUT\_TOKENS : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.
    
    Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses

Request JSON body:

    {
      "model": "MODEL",
      "input": "INPUT",
      "max_output_tokens": MAX_OUTPUT_TOKENS,
      "stream": true,
      "store": false
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"

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
        -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content

## Make a stateful call to the Responses API

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To use stateful functionalities, you must configure your [Organization Policy Service](https://docs.cloud.google.com/organization-policy/overview) to allow it. Specifically, update the constraint `constraints/vertexai.allowedPartnerModelFeatures` by adding `publishers/xai/models/ MODEL_NAME :stateful_responses_api` to the allowed values (for example, `publishers/xai/models/grok-4.20-reasoning:stateful_responses_api` ). For more information, see [Control model access](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/control-model-access) .

The Responses API supports multi-turn conversations through stateful requests. By default, `store` is set to `true` , which enables stateful responses. In a stateful conversation, you can reference a previous response by providing its `id` in the `previous_response_id` field.

> **Note:** Stateful responses are retained in Google-managed storage for **30 days** . You can use the response ID to retrieve or continue a conversation within **30 days** of sending the request. When a response is referenced by a new request (through `previous_response_id` ), the conversational context is carried forward into the new response, ensuring the history remains available while the conversation is active.

The following samples show a two-turn conversation using the Responses API:

### Turn 1: Initial request

In the first turn, make a request with `store` set to `true` . You can also omit the `store` parameter because `true` is the default value.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    from openai import OpenAI
    client = OpenAI()
    response = client.responses.create(
        model="MODEL",
        input="randomly pick 3 colors, just return the words of the colors",
    )
    print(response)

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses

Request JSON body:

    {
      "model": "MODEL",
      "input": "randomly pick 3 colors, just return the words of the colors"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"

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
        -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content

The following example shows a complete curl request:

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
      -d '{
        "model": "xai/grok-4.20-reasoning",
        "input": "randomly pick 3 colors, just return the words of the colors"
      }'

Example response for Turn 1:

    {
      "background": false,
      "completed_at": 1780435592,
      "created_at": 1780435591,
      "error": null,
      "frequency_penalty": 0,
      "id": "hkofavjWJuaRifEPntCBiA8",
      "incomplete_details": null,
      "instructions": null,
      "max_output_tokens": null,
      "max_tool_calls": null,
      "metadata": {
        "system_fingerprint": "fp_39c5j0a3e9"
      },
      "model": "xai/grok-4.20-reasoning",
      "object": "response",
      "output": [
        {
          "content": [
            {
              "annotations": [],
              "logprobs": [],
              "text": "violet teal crimson",
              "type": "output_text"
            }
          ],
          "id": "msg_hkofavjWJuaRifEPntCBiA8",
          "role": "assistant",
          "status": "completed",
          "type": "message"
        }
      ],
      "parallel_tool_calls": true,
      "presence_penalty": 0,
      "previous_response_id": null,
      "prompt_cache_key": null,
      "reasoning": {
        "effort": "medium",
        "summary": "detailed"
      },
      "safety_identifier": null,
      "service_tier": "default",
      "status": "completed",
      "store": true,
      "temperature": 0.7,
      "text": {
        "format": {
          "type": "text"
        }
      },
      "tool_choice": "auto",
      "tools": [],
      "top_logprobs": 0,
      "top_p": 0.95,
      "truncation": "disabled",
      "usage": {
        "extra_properties": {
          "google": {
            "traffic_type": "ON_DEMAND"
          }
        },
        "input_tokens": 343,
        "input_tokens_details": {
          "cached_tokens": 320
        },
        "num_server_side_tools_used": 0,
        "num_sources_used": 0,
        "output_tokens": 389,
        "output_tokens_details": {
          "reasoning_tokens": 386
        },
        "total_tokens": 732
      },
      "user": null
    }

### Turn 2: Follow-up request

In the second turn, reference the ID from the previous response in the `previous_response_id` parameter.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    from openai import OpenAI
    client = OpenAI()
    response = client.responses.create(
        model="MODEL",
        input="What is the second color?",
        previous_response_id="PREVIOUS_RESPONSE_ID",
    )
    print(response)

  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .
  - PREVIOUS\_RESPONSE\_ID : The ID of the previous response to continue the conversation.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - MODEL : The model name you want to use, for example `xai/grok-4.20-reasoning` .
  - PREVIOUS\_RESPONSE\_ID : The ID of the previous response.

HTTP method and URL:

    POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses

Request JSON body:

    {
      "model": "MODEL",
      "input": "What is the second color?",
      "previous_response_id": "PREVIOUS_RESPONSE_ID"
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"

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
        -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content

The following example shows a complete curl request:

    curl -X POST \
      -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
      -d '{
        "model": "xai/grok-4.20-reasoning",
        "input": "What is the second color?",
        "previous_response_id": "hkofavjWJuaRifEPntCBiA8"
      }'

Example response for Turn 2:

    {
      "background": false,
      "completed_at": 1780436062,
      "created_at": 1780436060,
      "error": null,
      "frequency_penalty": 0,
      "id": "VkwfatGAFY2CifEPvPu-iQM",
      "incomplete_details": null,
      "instructions": null,
      "max_output_tokens": null,
      "max_tool_calls": null,
      "metadata": {
        "system_fingerprint": "fp_39c5j0a3e9"
      },
      "model": "xai/grok-4.20-reasoning",
      "object": "response",
      "output": [
        {
          "content": [
            {
              "annotations": [],
              "logprobs": [],
              "text": "teal",
              "type": "output_text"
            }
          ],
          "id": "msg_VkwfatGAFY2CifEPvPu-iQM",
          "role": "assistant",
          "status": "completed",
          "type": "message"
        }
      ],
      "parallel_tool_calls": true,
      "presence_penalty": 0,
      "previous_response_id": "hkofavjWJuaRifEPntCBiA8",
      "prompt_cache_key": null,
      "reasoning": {
        "effort": "medium",
        "summary": "detailed"
      },
      "safety_identifier": null,
      "service_tier": "default",
      "status": "completed",
      "store": true,
      "temperature": 0.7,
      "text": {
        "format": {
          "type": "text"
        }
      },
      "tool_choice": "auto",
      "tools": [],
      "top_logprobs": 0,
      "top_p": 0.95,
      "truncation": "disabled",
      "usage": {
        "extra_properties": {
          "google": {
            "traffic_type": "ON_DEMAND"
          }
        },
        "input_tokens": 360,
        "input_tokens_details": {
          "cached_tokens": 320
        },
        "num_server_side_tools_used": 0,
        "num_sources_used": 0,
        "output_tokens": 314,
        "output_tokens_details": {
          "reasoning_tokens": 312
        },
        "total_tokens": 674
      },
      "user": null
    }

### Get a response

> **Note:** Retrieving responses by ID is available in the `v1beta1` API version and is in Public Preview.

You can retrieve a previously generated response by its ID.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    import json
    import openai
    v1beta1_client = openai.OpenAI(
        base_url=f"https://aiplatform.googleapis.com/v1beta1/projects/{project_id}/locations/global/endpoints/openapi",
        api_key=credentials.token,
    )
    
    response_id = "RESPONSE_ID"
    retrieved_response = v1beta1_client.responses.retrieve(response_id)
    
    print(json.dumps(retrieved_response.model_dump(), indent=2))

  - RESPONSE\_ID : The ID of the response to retrieve.

Example response:

    {
      "id": "pfgxarvYI4C0hMIP-qns4AU",
      "created_at": 1781659813.0,
      "error": null,
      "incomplete_details": null,
      "instructions": null,
      "metadata": {
        "system_fingerprint": "fp_39c5j0a3e9"
      },
      "model": "xai/grok-4.20-reasoning",
      "object": "response",
      "output": [
        {
          "id": "msg_pfgxarvYI4C0hMIP-qns4AU",
          "content": [
            {
              "annotations": [],
              "text": "Once upon a twilight meadow, a gentle unicorn named Luna followed a trail of glowing fireflies to her mossy bed beneath the silver moon, where she dreamed of rainbow bridges and endless starlit gallops.",
              "type": "output_text",
              "logprobs": []
            }
          ],
          "role": "assistant",
          "status": "completed",
          "type": "message",
          "phase": null
        }
      ],
      "parallel_tool_calls": true,
      "temperature": 0.7,
      "tool_choice": "auto",
      "tools": [],
      "top_p": 0.95,
      "background": false,
      "completed_at": 1781659815.0,
      "conversation": null,
      "max_output_tokens": null,
      "max_tool_calls": null,
      "moderation": null,
      "previous_response_id": null,
      "prompt": null,
      "prompt_cache_key": null,
      "prompt_cache_retention": null,
      "reasoning": {
        "effort": "medium",
        "generate_summary": null,
        "summary": "detailed"
      },
      "safety_identifier": null,
      "service_tier": "default",
      "status": "completed",
      "text": {
        "format": {
          "type": "text"
        },
        "verbosity": null
      },
      "top_logprobs": 0,
      "truncation": "disabled",
      "usage": {
        "input_tokens": 340,
        "input_tokens_details": {
          "cached_tokens": 0
        },
        "output_tokens": 375,
        "output_tokens_details": {
          "reasoning_tokens": 334
        },
        "total_tokens": 715,
        "extra_properties": {
          "google": {
            "traffic_type": "ON_DEMAND"
          }
        },
        "num_server_side_tools_used": 0,
        "num_sources_used": 0
      },
      "user": null,
      "frequency_penalty": 0,
      "presence_penalty": 0,
      "store": true
    }

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - RESPONSE\_ID : The ID of the response to retrieve.

HTTP method and URL:

    GET https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X GET \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method GET `
        -Headers $headers `
        -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID" | Select-Object -Expand Content

The following example shows a complete curl request:

    curl -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
      -H "Content-Type: application/json" \
      "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/VkwfatGAFY2CifEPvPu-iQM"

Example response:

    {
      "background": false,
      "completed_at": 1780436062,
      "created_at": 1780436060,
      "error": null,
      "frequency_penalty": 0,
      "id": "VkwfatGAFY2CifEPvPu-iQM",
      "incomplete_details": null,
      "instructions": null,
      "max_output_tokens": null,
      "max_tool_calls": null,
      "metadata": {
        "system_fingerprint": "fp_39c5j0a3e9"
      },
      "model": "xai/grok-4.20-reasoning",
      "object": "response",
      "output": [
        {
          "content": [
            {
              "annotations": [],
              "logprobs": [],
              "text": "teal",
              "type": "output_text"
            }
          ],
          "id": "msg_VkwfatGAFY2CifEPvPu-iQM",
          "role": "assistant",
          "status": "completed",
          "type": "message"
        }
      ],
      "parallel_tool_calls": true,
      "presence_penalty": 0,
      "previous_response_id": "hkofavjWJuaRifEPntCBiA8",
      "prompt_cache_key": null,
      "reasoning": {
        "effort": "medium",
        "summary": "detailed"
      },
      "safety_identifier": null,
      "service_tier": "default",
      "status": "completed",
      "store": true,
      "temperature": 0.7,
      "text": {
        "format": {
          "type": "text"
        }
      },
      "tool_choice": "auto",
      "tools": [],
      "top_logprobs": 0,
      "top_p": 0.95,
      "truncation": "disabled",
      "usage": {
        "extra_properties": {
          "google": {
            "traffic_type": "ON_DEMAND"
          }
        },
        "input_tokens": 360,
        "input_tokens_details": {
          "cached_tokens": 320
        },
        "num_server_side_tools_used": 0,
        "num_sources_used": 0,
        "output_tokens": 314,
        "output_tokens_details": {
          "reasoning_tokens": 312
        },
        "total_tokens": 674
      },
      "user": null
    }

### Delete a response

> **Note:** Deleting responses by ID is available in the `v1beta1` API version and is in Public Preview.

You can delete a previously generated response by its ID.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

    import openai
    v1beta1_client = openai.OpenAI(
        base_url=f"https://aiplatform.googleapis.com/v1beta1/projects/{project_id}/locations/global/endpoints/openapi",
        api_key=credentials.token,
    )
    
    response_id = "RESPONSE_ID"
    delete_response = v1beta1_client.responses.delete(response_id)
    
    print(delete_response)

  - RESPONSE\_ID : The ID of the response to delete.

Example response:

    {
      "deleted": true,
      "id": "TekCarmCCOPYyOgPnrWSgAY",
      "object": "response"
    }

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your Google Cloud project ID.
  - RESPONSE\_ID : The ID of the response to delete.

HTTP method and URL:

    DELETE https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    curl -X DELETE \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID"

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method DELETE `
        -Headers $headers `
        -Uri "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID" | Select-Object -Expand Content

The following example shows a complete curl request:

    curl -X DELETE 
    
      -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" 
    
      -H "Content-Type: application/json" 
    
      "https://aiplatform.googleapis.com/v1beta1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/TekCarmCCOPYyOgPnrWSgAY"

Example response:

    {
      "deleted": true,
      "id": "TekCarmCCOPYyOgPnrWSgAY",
      "object": "response"
    }

## What's next

  - Learn more about [Grok models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok) .
  - Learn how to use [Function calling with the Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/function-calling#responses-api) .
  - Learn how to use [Structured output with the Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/structured-output#responses-api) .
