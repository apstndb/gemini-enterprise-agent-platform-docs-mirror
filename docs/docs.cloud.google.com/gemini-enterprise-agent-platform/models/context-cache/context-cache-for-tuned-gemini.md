---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-for-tuned-gemini
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-for-tuned-gemini
title: Context Caching for Fine-tuned Gemini Models
description: Learn how to use context caching for your fine-tuned Gemini models to improve performance and reduce costs for prompts that include large amounts of context.
data_source: docs.cloud.google.com
---

You can use context caching for your fine-tuned Gemini models to improve performance and reduce costs for prompts that include large amounts of context. By caching frequently used context, you avoid re-sending large amounts of data with each request to your fine-tuned model.

The management operations ( `Read` , `Update` , `Delete` ) of the context cache for tuned Gemini models remain consistent with base models. Only cached content creation and inference require specific adjustment, which is detailed in the following sections.

## Prerequisites

**Fine-tuning a Gemini Model:** You need a deployed fine-tuned Gemini model based on a supported base model (see [Context caching overview](https://docs.cloud.google.com/vertex-ai/docs/context-cache/context-cache-overview#supported_models) ). For details on how to fine-tune a Gemini model, see [Fine-tune a Gemini model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini-use-supervised-tuning) . To get the endpoint for your deployed tuned model, see [Deploy a tuned model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/overview#deploy_a_tuned_model) .

Make sure that you have the following information:

  - The ID and the version of the tuned Gemini model
  - The endpoint resource name for the deployed fine-tuned model

## Supported versions

Fine-tuned Gemini models support implicit caching for the following versions:

  - [Gemini 3.1 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-pro)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-flash-lite)
  - [Gemini 3 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-pro)
  - [Gemini 3 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-flash)
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash-lite)

Explicit caching is supported for the following versions:

  - [Gemini 3.1 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-pro)
  - [Gemini 3.1 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-1-flash-lite)
  - [Gemini 3 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-pro)
  - [Gemini 3 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/3-flash)
  - [Gemini 2.5 Pro](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-pro)
  - [Gemini 2.5 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash)
  - [Gemini 2.5 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-5-flash-lite)
  - [Gemini 2.0 Flash](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-0-flash)
  - [Gemini 2.0 Flash-Lite](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/gemini/2-0-flash-lite)

## Create a context cache for a fine-tuned model

The procedure for creating a context cache for a fine-tuned model largely follows the steps outlined in [Create a context cache](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-create) . Consult the linked documentation for the general process; this guide focuses on the difference of creating context cache for fine-tuned Gemini models.

Instead of using the base model in the form of `projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}` , you must use your fine-tuned model in the form of `projects/{PROJECT}/locations/{LOCATION}/models/{MODEL}@{VERSION}` .

The following examples show how to create a context cache with a tuned Gemini model.

### REST

You can use REST to create a context cache by using the Agent Platform API to send a POST request to the publisher model endpoint. The following example shows how to create a context cache using a file stored in a Cloud Storage bucket.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region to process the request and where the cached content is stored. For a list of supported regions, see [Available regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/locations) .
  - MODEL\_ID : The fine-tuned Gemini model ID.
  - MODEL\_VERSION : The fine-tuned Gemini model version.
  - CACHE\_DISPLAY\_NAME : A meaningful display name to describe and to help you identify each context cache.
  - MIME\_TYPE : The MIME type of the content to cache.
  - CONTENT\_TO\_CACHE\_URI : The Cloud Storage URI of the content to cache.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/cachedContents

Request JSON body:

    {
      "model": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID@MODEL_VERSION",
      "displayName": "CACHE_DISPLAY_NAME",
      "contents": [{
        "role": "user",
          "parts": [{
            "fileData": {
              "mimeType": "MIME_TYPE",
              "fileUri": "CONTENT_TO_CACHE_URI"
            }
          }]
      }]
    }

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/cachedContents"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/cachedContents" | Select-Object -Expand Content

You should receive a JSON response similar to the following:

#### Response

    {
      "name": "projects/PROJECT_NUMBER/locations/us-central1/cachedContents/CACHE_ID",
      "model": "projects/PROJECT_ID/locations/LOCATION/models/MODEL_ID@MODEL_VERSION",
      "createTime": "2024-06-04T01:11:50.808236Z",
      "updateTime": "2024-06-04T01:11:50.808236Z",
      "expireTime": "2024-06-04T02:11:50.794542Z"
    }

### Example curl command

    LOCATION="us-central1"
    MODEL_ID="model-id"
    PROJECT_ID="test-project"
    MODEL_VERSION=1
    MIME_TYPE="video/mp4"
    CACHED_CONTENT_URI="gs://path-to-bucket/video-file-name.mp4"
    
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/cachedContents -d \
    '{
      "model":"projects/${PROJECT_ID}/locations/${LOCATION}/models/${MODEL_ID}@${MODEL_VERSION}",
      "contents": [
        {
          "role": "user",
          "parts": [
            {
              "fileData": {
                "mimeType": "${MIME_TYPE}",
                "fileUri": "${CACHED_CONTENT_URI}"
              }
            }
          ]
        }
      ]
    }'

## Use a context cache for a fine-tuned model

The procedure for using a context cache for a fine-tuned model largely follows the steps outlined in [Use a context cache](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-use) . Consult the linked documentation for the general process; this guide focuses on the difference of using context cache for fine-tuned Gemini models.

Instead of sending the request to the base model endpoint in the form of `projects/{PROJECT}/locations/{LOCATION}/publishers/google/models/{MODEL}` , you must send it to the endpoint of your deployed fine-tuned model in the form of `projects/{PROJECT}/locations/{LOCATION}/endpoints/{ENDPOINT_ID}` .

The following code example shows how to use a context cache with a tuned Gemini model.

When you use a context cache, you can't specify the following properties:

  - `GenerativeModel.system_instructions`
  - `GenerativeModel.tool_config`
  - `GenerativeModel.tools`

### REST

You can use REST to specify a context cache with a prompt by using the Agent Platform API to send a POST request to the publisher model endpoint.

Before using any of the request data, make the following replacements:

  - PROJECT\_ID : Your \[project ID\](/resource-manager/docs/creating-managing-projects\#identifiers). .
  - LOCATION : The region where the request to [create the context cache](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-create) was processed.
  - ENDPOINT\_ID : The endpoint where the fine-tuned model is deployed.
  - PROMPT\_TEXT : The text prompt to submit to the model.

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:generateContent

Request JSON body:

    {
      "cachedContent": "projects/PROJECT_NUMBER/locations/LOCATION/cachedContents/CACHE_ID",
      "contents": [
          {"role":"user","parts":[{"text":"PROMPT_TEXT"}]}
      ],
      "generationConfig": {
          "maxOutputTokens": 8192,
          "temperature": 1,
          "topP": 0.95,
      },
      "safetySettings": [
          {
              "category": "HARM_CATEGORY_HATE_SPEECH",
              "threshold": "BLOCK_MEDIUM_AND_ABOVE"
          },
          {
              "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
              "threshold": "BLOCK_MEDIUM_AND_ABOVE"
          },
          {
              "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
              "threshold": "BLOCK_MEDIUM_AND_ABOVE"
          },
          {
              "category": "HARM_CATEGORY_HARASSMENT",
              "threshold": "BLOCK_MEDIUM_AND_ABOVE"
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
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:generateContent"

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
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/endpoints/ENDPOINT_ID:generateContent" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "candidates": [
        {
          "content": {
            "role": "model",
            "parts": [
              {
                "text": "MODEL_RESPONSE"
              }
            ]
          },
          "finishReason": "STOP",
          "safetyRatings": [
            {
              "category": "HARM_CATEGORY_HATE_SPEECH",
              "probability": "NEGLIGIBLE",
              "probabilityScore": 0.21866937,
              "severity": "HARM_SEVERITY_NEGLIGIBLE",
              "severityScore": 0.19946389
            },
            {
              "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
              "probability": "MEDIUM",
              "probabilityScore": 0.6880493,
              "severity": "HARM_SEVERITY_MEDIUM",
              "severityScore": 0.43374163
            },
            {
              "category": "HARM_CATEGORY_HARASSMENT",
              "probability": "NEGLIGIBLE",
              "probabilityScore": 0.4442634,
              "severity": "HARM_SEVERITY_LOW",
              "severityScore": 0.37903354
            },
            {
              "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
              "probability": "NEGLIGIBLE",
              "probabilityScore": 0.10502681,
              "severity": "HARM_SEVERITY_LOW",
              "severityScore": 0.28170192
            }
          ]
        }
      ],
      "usageMetadata": {
        "promptTokenCount": 55927,
        "candidatesTokenCount": 105,
        "totalTokenCount": 56032
      }
    }

### Example curl command

    LOCATION="us-central1"
    PROJECT_ID="test-project"
    ENDPOINT_ID=987654321
    
    curl -X POST \
    -H "Authorization: Bearer $(gcloud auth print-access-token)" \
    -H "Content-Type: application/json" \
    "https://${LOCATION}-aiplatform.googleapis.com/v1/projects/${PROJECT_ID}/locations/${LOCATION}/endpoints/${ENDPOINT_ID}:generateContent" -d \
    '{
      "cachedContent": "projects/${PROJECT_NUMBER}/locations/${LOCATION}/cachedContents/${CACHE_ID}",
      "contents": [
          {"role":"user","parts":[{"text":"What are the benefits of exercise?"}]}
      ],
      "generationConfig": {
          "maxOutputTokens": 8192,
          "temperature": 1,
          "topP": 0.95,
      },
      "safetySettings": [
        {
          "category": "HARM_CATEGORY_HATE_SPEECH",
          "threshold": "BLOCK_MEDIUM_AND_ABOVE"
        },
        {
          "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
          "threshold": "BLOCK_MEDIUM_AND_ABOVE"
        },
        {
          "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
          "threshold": "BLOCK_MEDIUM_AND_ABOVE"
        },
        {
          "category": "HARM_CATEGORY_HARASSMENT",
          "threshold": "BLOCK_MEDIUM_AND_ABOVE"
        }
      ],
    }'
