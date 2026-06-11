---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-exa
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/grounding/grounding-with-exa
title: Grounding with Exa web search
description: Implement Gemini model grounding with Exa's web search API. Access real-time public web data for factual, current generative AI.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

[Exa](https://exa.ai/) provides a search API that gives access to publicly available web data optimized for grounding large language model responses. This page explains how to ground Gemini responses by using Exa.

Grounding with Exa web search on Gemini Enterprise Agent Platform is a Separate Offering (as defined in your Google Cloud Agreement) that connects Gemini models to public web data provided by [Exa's search API](https://exa.ai/docs/reference/search-api-guide) .

> **Note:** For web publishers, grounding with Exa on Gemini Enterprise Agent Platform respects opt-out signals such as "noindex" tags. Web publishers can manage their opt-out preferences by following the instructions in the [Exa documentation](https://exa.ai/docs/reference/faqs#does-exa-have-a-crawler) .

## Use cases

Grounding with Exa improves accuracy and reduces hallucinations by giving models access to fresh, relevant web data. Common use cases include:

  - **General agents and chatbots** : Retrieve up-to-date information to produce more reliable answers.
  - **Research agents** : Conduct deep web research across multiple sources.
  - **Coding agents** : Pull the latest code snippets, documents, and technical references.
  - **Voice agents** : Web retrieval to support real-time, low-latency voice interactions.
  - **Vertical-specific agents** : Fetch up-to-date, domain-specific information tailored to a particular industry or knowledge vertical.
  - **Data enrichment** : Augment internal datasets with current web context and metadata.
  - **Automated workflows** : Periodically gather news, people, company, or other frequently updated data for internal or production workflows.

**Example**

*Who won Superbowl 2026?*

| Without Grounding                                                             | With Grounding                                                                                                                                                         |
| ----------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| I cannot tell you who won Super Bowl 2026 as that event has not happened yet. | The Seattle Seahawks won Super Bowl LX on February 8, 2026, defeating the New England Patriots with a final score of 29-13. **Sources:** domain1.com, domain2.com, ... |

## Supported models

This section lists the models that support Grounding with Exa web search.

## Before you begin

To use Grounding with Exa, you need to get an API key from [Exa's web site](https://exa.ai/docs/reference/search-api-guide) . This API key is used in your request to Gemini.

## Ground Gemini responses with Exa

Request grounded responses from Gemini by using the REST API as follows. For best performance, we recommend using default settings for optional parameters unless you strictly require non-default values.

### REST

Before using any of the request data, make the following replacements:

  - LOCATION : The region to process the request. To use the global endpoint, exclude the location from the endpoint name and configure the location of the resource to \`global\`.
  - PROJECT\_ID : Your Google Cloud project ID.
  - MODEL\_ID : The ID of the model to use.
  - TEXT : The text prompt to send to the model.
  - API\_KEY : Your API key for Exa web search.
  - SEARCH\_TYPE : Optional: The type of Exa search to run. Valid values are `auto` (the default) and `fast` . `fast` runs with lower latency at the cost of a less comprehensive search.
  - EXCLUDE\_DOMAINS : Optional: List of domains to exclude from search results. If specified, no results will be returned from these domains. You can specify up to 1200 domains.
  - INCLUDE\_DOMAINS : Optional: List of domains to include in the search. If specified, results will only come from these domains. You can specify up to 1200 domains.
  - MAX\_CHARACTERS : Optional: Maximum number of characters to return for highlights. Controls the total length of highlight text returned per URL.
  - NUM\_RESULTS : Optional: The maximum number of search results to use for grounding. If not specified, defaults to `5` .

HTTP method and URL:

    POST https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:generateContent

Request JSON body:

    {
      "contents": [{
        "role": "user",
        "parts": [{
          "text": "TEXT"
        }]
      }],
      "tools": [{
        "exaAiSearch": {
            "api_key": "API_KEY",
            "customConfigs": {
                "type": "SEARCH_TYPE",
                "excludeDomains": ["EXCLUDE_DOMAINS"],
                "includeDomains": ["INCLUDE_DOMAINS"],
                "contents": {
                    "highlights": {
                        "maxCharacters": MAX_CHARACTERS
                    }
                },
                "numResults": NUM_RESULTS
            }
        }
    }],
      "model": "projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID"
    }

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    curl -X POST \
         -H "Authorization: Bearer $(gcloud auth print-access-token)" \
         -H "Content-Type: application/json; charset=utf-8" \
         -d @request.json \
         "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:generateContent"

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

    $cred = gcloud auth print-access-token
    $headers = @{ "Authorization" = "Bearer $cred" }
    
    Invoke-WebRequest `
        -Method POST `
        -Headers $headers `
        -ContentType: "application/json; charset=utf-8" `
        -InFile request.json `
        -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:generateContent" | Select-Object -Expand Content

You should receive a JSON response similar to the following.

#### Response

    {
      "candidates": [
        {
          "content": {
            "role": "model",
            "parts": [
              {
                "text": "The Seattle Seahawks won Super Bowl LX on February 8, 2026, defeating the New England Patriots with a final score of 29-13."
              }
            ]
          },
          "finishReason": "STOP",
          "groundingMetadata": {
            "webSearchQueries": [
              "who won the last super bowl"
            ],
            "groundingChunks": [
              {
                "web": {
                  "uri": "https://...",
                  "title": "Super Bowl LX",
                  "domain": "domain.com"
                }
              },
              {
                "web": {
                  "uri": "https://...",
                  "title": "Super Bowl LX Results",
                  "domain": "domain.com"
                }
              }
            ],
            "groundingSupports": [
              {
                "segment": {
                  "endIndex": 125,
                  "text": "The Seattle Seahawks won Super Bowl LX on February 8, 2026, defeating the New England Patriots with a final score of 29-13."
                },
                "groundingChunkIndices": [
                  0,
                  1
                ]
              }
            ]
          }
        }
      ],
      "usageMetadata": {
        "promptTokenCount": 33,
        "candidatesTokenCount": 106,
        "totalTokenCount": 284,
        "billablePromptUsage": {
          "textCount": 142
        },
        "trafficType": "ON_DEMAND",
        "promptTokensDetails": [
          {
            "modality": "TEXT",
            "tokenCount": 33
          }
        ],
        "candidatesTokensDetails": [
          {
            "modality": "TEXT",
            "tokenCount": 106
          }
        ],
        "toolUsePromptTokensDetails": [
          {
            "modality": "TEXT",
            "tokenCount": 39
          }
        ],
        "toolUsePromptTokenCount": 39,
        "thoughtsTokenCount": 106
      },
      "modelVersion": "MODEL_VERSION",
      "createTime": "CREATE_TIME",
      "responseId": "RESPONSE_ID"
    }

## Quota

The default quota is 200 prompts per minute. If you need to increase your rate limits, contact <support@exa.ai> and your Google account team with your use case and requirements.

## Billing

The use of Grounding with Exa incurs the following charges:

  - **Gemini token consumption** : Prompt tokens, thinking tokens, output tokens. For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
  - **Gemini's Grounding with your data** : For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .
  - **Pricing for the use of Exa's search API** : For more information, see [Exa's pricing page](https://exa.ai/pricing) .
