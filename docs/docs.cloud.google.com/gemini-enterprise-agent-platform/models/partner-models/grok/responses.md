---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/responses
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/responses
title: Call Responses API
description: Call XAI Grok models using the Responses API. Implement requests to generate responses.
data_source: docs.cloud.google.com
---

XAI's Grok models on Gemini Enterprise Agent Platform support the [Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1beta1/projects.locations.endpoints.responses) for generating responses.

This page shows how to make calls to Grok models using the Responses API.

## Before you begin

To use Grok models with Gemini Enterprise Agent Platform, you must perform the following steps. The Gemini Enterprise Agent Platform API ( `aiplatform.googleapis.com` ) must be enabled.

## Make a stateless call to the Responses API

The default value for `store` is `false` , so requests are stateless unless you set `store` to `true` . The following samples set `store` to `false` (or `False` in Python) explicitly.

### Make a non-streaming call to the Responses API

The following samples show how to make a non-streaming call to the Responses API:

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
response = client.responses.create(
    model="MODEL",
    input="INPUT",
    max_output_tokens=MAX_OUTPUT_TOKENS,
    stream=False,
    store=False,
)
print(response)
```

- ` PROJECT_ID ` : Your Google Cloud project ID.

- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

- ` INPUT ` : The prompt or input for the model.

- ` MAX_OUTPUT_TOKENS ` : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.

  Specify a lower value for shorter responses and a higher value for potentially longer responses.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.

- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

- ` INPUT ` : The prompt or input for the model.

- ` MAX_OUTPUT_TOKENS ` : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.

  Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses
```

Request JSON body:

```
{
  "model": "MODEL",
  "input": "INPUT",
  "max_output_tokens": MAX_OUTPUT_TOKENS,
  "stream": false,
  "store": false
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content
```

The following example shows a complete curl request:

```
curl -s -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
  -d '{
    "model": "xai/grok-4.7",
    "input": "Explain black holes in one short sentence.",
    "max_output_tokens": 100,
    "stream": false,
    "store": false
  }'
```

Based on the Responses API definition, a non-streaming response will contain a unique ID, model metadata, usage statistics, and an output array containing the generated text.

```
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
```

### Make a streaming call to the Responses API

The following samples show how to make a streaming call to the Responses API:

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
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
```

- ` PROJECT_ID ` : Your Google Cloud project ID.

- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

- ` INPUT ` : The prompt or input for the model.

- ` MAX_OUTPUT_TOKENS ` : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.

  Specify a lower value for shorter responses and a higher value for potentially longer responses.

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.

- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

- ` INPUT ` : The prompt or input for the model.

- ` MAX_OUTPUT_TOKENS ` : Maximum number of tokens that can be generated in the response. A token is approximately four characters. 100 tokens correspond to roughly 60-80 words.

  Specify a lower value for shorter responses and a higher value for potentially longer responses.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses
```

Request JSON body:

```
{
  "model": "MODEL",
  "input": "INPUT",
  "max_output_tokens": MAX_OUTPUT_TOKENS,
  "stream": true,
  "store": false
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content
```

## Make a stateful call to the Responses API

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

To make stateful requests, you must configure your [Organization Policy Service](https://docs.cloud.google.com/organization-policy/overview) to allow them. Specifically, update the constraint `constraints/vertexai.allowedPartnerModelFeatures` by adding `publishers/xai/models/ `` MODEL_NAME `` :stateful_responses_api` to the allowed values (for example, `publishers/xai/models/grok-4.7:stateful_responses_api` ). For more information, see [Control model access](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

The Responses API supports multi-turn conversations through stateful requests. The default value for `store` is `false` , so to make a stateful request you must explicitly set `store` to `true` . In a stateful conversation, you can reference a previous response by providing its `id` in the `previous_response_id` field.

> **Note:** Stateful responses are retained in Google-managed storage for **30 days** . You can use the response ID to retrieve or continue a conversation within **30 days** of sending the request. When a response is referenced by a new request (through `previous_response_id` ), the conversational context is carried forward into the new response, ensuring the history remains available while the conversation is active.

### Create a response

The following samples show a two-turn conversation using the Responses API:

**Turn 1: Initial request**

In the first turn, make a request with `store` set to `true` . If you omit the `store` parameter, it defaults to `false` and the response isn't stored.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
response = client.responses.create(
    model="MODEL",
    input="randomly pick 3 colors, just return the words of the colors",
    store=True,
)
print(response)
```

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

Example response for Turn 1:

```
{
  "background": false,
  "completed_at": 1793834418,
  "created_at": 1793834418,
  "error": null,
  "frequency_penalty": 0,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "cerulean amber violet",
          "type": "output_text"
        }
      ],
      "id": "msg_5f76a045-71d9-45af-8b07-1f2feae0675a",
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
    "effort": "high",
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
    "context_details": {
      "input_tokens": 220,
      "output_tokens": 144
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 220,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 144,
    "output_tokens_details": {
      "reasoning_tokens": 139
    },
    "total_tokens": 364
  },
  "user": null
}
```

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses
```

Request JSON body:

```
{
  "model": "MODEL",
  "input": "randomly pick 3 colors, just return the words of the colors",
  "store": true
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content
```

The following example shows a complete curl request:

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
  -d '{
    "model": "xai/grok-4.7",
    "input": "randomly pick 3 colors, just return the words of the colors",
    "store": true
  }'
```

Example response for Turn 1:

```
{
  "background": false,
  "completed_at": 1793834418,
  "created_at": 1793834418,
  "error": null,
  "frequency_penalty": 0,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "cerulean amber violet",
          "type": "output_text"
        }
      ],
      "id": "msg_5f76a045-71d9-45af-8b07-1f2feae0675a",
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
    "effort": "high",
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
    "context_details": {
      "input_tokens": 220,
      "output_tokens": 144
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 220,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 144,
    "output_tokens_details": {
      "reasoning_tokens": 139
    },
    "total_tokens": 364
  },
  "user": null
}
```

**Turn 2: Follow-up request**

In the second turn, reference the ID from the previous response in the `previous_response_id` parameter. Set `store` to `true` if you want to store this response as well, for example to continue the conversation or retrieve it later.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
response = client.responses.create(
    model="MODEL",
    input="What is the second color?",
    previous_response_id="PREVIOUS_RESPONSE_ID",
    store=True,
)
print(response)
```

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .
- ` PREVIOUS_RESPONSE_ID ` : The ID of the previous response to continue the conversation.

Example response for Turn 2:

```
{
  "background": false,
  "completed_at": 1793835029,
  "created_at": 1793835029,
  "error": null,
  "frequency_penalty": 0,
  "id": "ee8b6aa6-777e-4aa2-8db4-46bbfe84491b",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "amber",
          "type": "output_text"
        }
      ],
      "id": "msg_ee8b6aa6-777e-4aa2-8db4-46bbfe84491b",
      "role": "assistant",
      "status": "completed",
      "type": "message"
    }
  ],
  "parallel_tool_calls": true,
  "presence_penalty": 0,
  "previous_response_id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "prompt_cache_key": null,
  "reasoning": {
    "effort": "high",
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
    "context_details": {
      "input_tokens": 239,
      "output_tokens": 41
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 239,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 41,
    "output_tokens_details": {
      "reasoning_tokens": 40
    },
    "total_tokens": 280
  },
  "user": null
}
```

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` MODEL ` : The model name you want to use, for example `xai/grok-4.7` .
- ` PREVIOUS_RESPONSE_ID ` : The ID of the previous response.

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses
```

Request JSON body:

```
{
  "model": "MODEL",
  "input": "What is the second color?",
  "previous_response_id": "PREVIOUS_RESPONSE_ID",
  "store": true
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" | Select-Object -Expand Content
```

The following example shows a complete curl request:

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses" \
  -d '{
    "model": "xai/grok-4.7",
    "input": "What is the second color?",
    "previous_response_id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
    "store": true
  }'
```

Example response for Turn 2:

```
{
  "background": false,
  "completed_at": 1793835029,
  "created_at": 1793835029,
  "error": null,
  "frequency_penalty": 0,
  "id": "ee8b6aa6-777e-4aa2-8db4-46bbfe84491b",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "amber",
          "type": "output_text"
        }
      ],
      "id": "msg_ee8b6aa6-777e-4aa2-8db4-46bbfe84491b",
      "role": "assistant",
      "status": "completed",
      "type": "message"
    }
  ],
  "parallel_tool_calls": true,
  "presence_penalty": 0,
  "previous_response_id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "prompt_cache_key": null,
  "reasoning": {
    "effort": "high",
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
    "context_details": {
      "input_tokens": 239,
      "output_tokens": 41
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 239,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 41,
    "output_tokens_details": {
      "reasoning_tokens": 40
    },
    "total_tokens": 280
  },
  "user": null
}
```

### Get a response

You can retrieve a previously generated response by its ID.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import json
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
response_id = "RESPONSE_ID"
retrieved_response = client.responses.retrieve(response_id)
print(json.dumps(retrieved_response.model_dump(), indent=2))
```

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` RESPONSE_ID ` : The ID of the response to retrieve.

Example response:

```
{
  "background": false,
  "completed_at": 1793834418,
  "created_at": 1793834418,
  "error": null,
  "frequency_penalty": 0,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "cerulean amber violet",
          "type": "output_text"
        }
      ],
      "id": "msg_5f76a045-71d9-45af-8b07-1f2feae0675a",
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
    "effort": "high",
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
    "context_details": {
      "input_tokens": 220,
      "output_tokens": 144
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 220,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 144,
    "output_tokens_details": {
      "reasoning_tokens": 139
    },
    "total_tokens": 364
  },
  "user": null
}
```

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` RESPONSE_ID ` : The ID of the response to retrieve.

HTTP method and URL:

```
GET https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID" | Select-Object -Expand Content
```

The following example shows a complete curl request:

```
curl -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/5f76a045-71d9-45af-8b07-1f2feae0675a"
```

Example response:

```
{
  "background": false,
  "completed_at": 1793834418,
  "created_at": 1793834418,
  "error": null,
  "frequency_penalty": 0,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "incomplete_details": null,
  "instructions": null,
  "max_output_tokens": null,
  "max_tool_calls": null,
  "metadata": {
    "system_fingerprint": "fp_grok47_0"
  },
  "model": "xai/grok-4.7",
  "object": "response",
  "output": [
    {
      "content": [
        {
          "annotations": [],
          "logprobs": [],
          "text": "cerulean amber violet",
          "type": "output_text"
        }
      ],
      "id": "msg_5f76a045-71d9-45af-8b07-1f2feae0675a",
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
    "effort": "high",
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
    "context_details": {
      "input_tokens": 220,
      "output_tokens": 144
    },
    "extra_properties": {
      "google": {
        "traffic_type": "ON_DEMAND"
      }
    },
    "input_tokens": 220,
    "input_tokens_details": {
      "cached_tokens": 0
    },
    "num_server_side_tools_used": 0,
    "num_sources_used": 0,
    "output_tokens": 144,
    "output_tokens_details": {
      "reasoning_tokens": 139
    },
    "total_tokens": 364
  },
  "user": null
}
```

### Delete a response

You can delete a previously generated response by its ID.

After you delete a response, you can't retrieve it or use its ID as the `previous_response_id` in a new request. Deleting a response doesn't remove its content from later responses in the same conversation: each response that references it through `previous_response_id` keeps that content as context until you delete that response too. To remove an entire conversation, delete every stored response in it.

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before running this sample, make sure to set the `OPENAI_BASE_URL` environment variable or set up oauth credentials. For more information, see [Authentication and credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/migrate/openai/auth-and-credentials) .

```
import google.auth
import google.auth.transport.requests
from openai import OpenAI
credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())
client = OpenAI(
    base_url="https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi",
    api_key=credentials.token,
)
response_id = "RESPONSE_ID"
delete_response = client.responses.delete(response_id)
print(delete_response)
```

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` RESPONSE_ID ` : The ID of the response to delete.

Example response:

```
{
  "deleted": true,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "object": "response"
}
```

### REST

After you set up your environment, you can use REST to test a text prompt. The following sample sends a request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID.
- ` RESPONSE_ID ` : The ID of the response to delete.

HTTP method and URL:

```
DELETE https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Execute the following command:

```
curl -X DELETE \
     -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID"
```

#### PowerShell

> **Note:** The following command uses Application Default Credentials. If you haven't set them up, run [`gcloud auth application-default login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/application-default/login) . For more information, see [Set up ADC for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Execute the following command:

```
$cred = gcloud auth application-default print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method DELETE `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/RESPONSE_ID" | Select-Object -Expand Content
```

The following example shows a complete curl request:

```
curl -X DELETE \
  -H "Authorization: Bearer $(gcloud auth application-default print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/endpoints/openapi/responses/5f76a045-71d9-45af-8b07-1f2feae0675a"
```

Example response:

```
{
  "deleted": true,
  "id": "5f76a045-71d9-45af-8b07-1f2feae0675a",
  "object": "response"
}
```

## What's next

- Learn more about [Grok models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok) .
- Learn how to use [Function calling with the Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/function-calling#responses-api) .
- Learn how to use [Structured output with the Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/grok/capabilities/structured-output#responses-api) .
