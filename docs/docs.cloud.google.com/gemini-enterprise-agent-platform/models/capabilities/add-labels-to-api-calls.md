---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls
title: Custom metadata labels
description: Add custom metadata labels to generateContent and streamGenerateContent API calls to organize calls and manage costs.
data_source: docs.cloud.google.com
---

You can add custom metadata to API calls like `generateContent` and `rawPredict` by using labels. This page explains what labels are, and shows you how to use them to break down your billed charges.

## What are labels?

A label is a key-value pair that you can assign to API calls like `generateContent` and `rawPredict` . They help you organize these calls and manage your usage and costs at scale, with the granularity you need. You can attach a label to each call, then filter the calls based on their labels. Information about labels is forwarded to the logging and billing system that lets you break down your usage and billed charges by label. With built-in [billing reports](https://docs.cloud.google.com/billing/docs/how-to/reports) , you can filter and group costs by labels. You can also use labels to query [billing data exports](https://docs.cloud.google.com/billing/docs/how-to/bq-examples) . For information on how to use labels after creation, see [an example from the labels overview](https://docs.cloud.google.com/resource-manager/docs/labels-overview#example) .

Agent Platform supports two kinds of labels: request body labels, which reach Cloud Billing, and header labels, which appear in inference request metadata logs. The next section compares them.

## Choose a label based on your use case

Agent Platform offers two label mechanisms. You set them differently, they reach different destinations, and they appear in different fields of the inference request metadata log. You can use either, or both on the same request when supported.

Request body labels work as follows:

- You set them in the `labels` field of the request body.
- They reach Cloud Billing and inference request metadata logs.
- They appear in the log entry's `labels` field.
- Supported on pay-as-you-go traffic.
- For partner models such as Claude, request labels are sent in the `X-Vertex-AI-Labels` header instead of the request body. They reach Cloud Billing but aren't written to the inference request metadata log.

Header labels work as follows:

- You set them in the `x-goog-agent-platform-observability-label-KEY` request header.
- They reach inference request metadata logs only.
- They appear in the log entry's `jsonPayload.httpHeaders` field.
- Supported API methods: `generateContent` and `streamGenerateContent` for Gemini models, and `rawPredict` and `streamRawPredict` for Claude models. Supported consumption options: Provisioned Throughput and every pay-as-you-go option that the model offers.

> **Note:** Header labels never reach Cloud Billing. If you need to break down billed charges, use request body labels.

## Find each label in the log entry

A single request can carry both. The following request sets one of each:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-2.5-pro:generateContent
x-goog-agent-platform-observability-label-team: payments

{
  "labels": {"cost_center": "cc-1234"},
  "contents": [{"role": "user", "parts": [{"text": "..."}]}]
}
```

The two labels land in different fields of the same log entry:

```
{
  "labels": {
    "gen_ai.operation.name": "generate_content",
    "cost_center": "cc-1234"
  },
  "jsonPayload": {
    "httpHeaders": {
      "x-goog-agent-platform-observability-label-team": {
        "values": ["payments"]
      }
    }
  }
}
```

The two label types occupy different fields, so you query them differently. In Logs Explorer:

```
labels.cost_center="cc-1234"
jsonPayload.httpHeaders."x-goog-agent-platform-observability-label-team".values="payments"
```

In Observability Analytics:

```
JSON_VALUE(labels.cost_center) AS cost_center,
JSON_VALUE(json_payload.httpHeaders
  ["x-goog-agent-platform-observability-label-team"].values[0]) AS team
```

## How header labels work

Header labels are part of inference request metadata logging. To capture them, [turn on inference request metadata logs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging#enable) for the project.

Send one header per label, using the reserved prefix. The prefix is case-insensitive:

```
x-goog-agent-platform-observability-label-KEY: VALUE
```

For example:

```
x-goog-agent-platform-observability-label-team: payments
x-goog-agent-platform-observability-label-application: invoice-ocr
```

Each header appears in the log entry under `jsonPayload.httpHeaders` , keyed by the lowercased header name, with the value in a `values` array, as shown in [Find each label in the log entry](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls#where-in-log) .

Agent Platform also captures a small set of its own headers: `x-vertex-ai-llm-request-type` and `x-vertex-ai-llm-shared-request-type` . No other headers are captured.

Header labels work the same way for Gemini and Claude, and they are how you label Claude requests in the inference request metadata log.

### Limits for header labels

- A single request writes at most 32 headers. When more are eligible, Agent Platform keeps them in ascending alphabetical order and drops the rest. The drop is silent.
- A header value longer than 1,024 bytes is truncated, and the truncation is marked in the stored value.
- Repeated headers of the same name are combined into a single entry with multiple values.

> **Caution:** The 32-header cap counts every captured header, not only your header labels. If your application already sends many headers, count them before you rely on header label attribution.

To query header labels, see [Usage by custom header label](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging#query-labels) .

## Requirements for labels

The labels applied to an API call must meet the following requirements:

- Each API call can have up to 64 labels for Google models and up to 32 labels for partner models.
- Each label must be a key-value pair.
- Keys have a minimum length of 1 character and a maximum length of 63 characters, and cannot be empty. Values can be empty, and have a maximum length of 63 characters.
- Keys and values can contain only lowercase letters, numeric characters, underscores, and dashes. All characters must use UTF-8 encoding, and international characters are allowed. Keys must start with a lowercase letter or international character.
- The key portion of a label must be unique within a single API call. However, you can use the same key with multiple calls.

These limits apply to the key and value for each label, and to the individual API call that have labels. There is no limit on how many label keys you can create across all API calls within a project. Each label key can have up to 1000 unique values across all requests over the life of the associated billing account. The label key might be dropped without notice if more than 1000 unique values are associated with it.

## Common uses of labels

Here are some common use cases for labels:

- **Team or cost center labels** : Add labels based on team or cost center to distinguish API calls owned by different teams (for example, `team:research` and `team:analytics` ). You can use this type of label for cost accounting or budgeting.

- **Component labels** : For example, `component:redis` , `component:frontend` , `component:ingest` , and `component:dashboard` .

- **Environment or stage labels** : For example, `environment:production` and `environment:test` .

- **Ownership labels** : Used to identify the teams that are responsible for operations, for example: `team:shopping-cart` .

> **Note:** Don't include sensitive information in labels, including personally identifiable information, such as an individual's name or title. Labels are not designed to handle sensitive information.

We recommend against creating large numbers of unique labels, such as for timestamps or individual values for every API call. The problem with this approach is that the keys clutter the catalog, increase load times significantly during queries, and make it difficult to effectively filter and report on API calls.

## Supported models for request labels

Request labels and header labels are supported on different models. The ability to add request labels to a request is supported for Google models and a subset of partner models. If you add request labels to a request for an unsupported model, the request results in an error. Google models take request labels in the `labels` field of the request body. Partner models take them in the `X-Vertex-AI-Labels` header.

### Google models

Google models support labels on the following API methods.

- `generateContent`
- `streamGenerateContent`

### Partner models

Partner models support labels on the following API methods.

- `rawPredict`
- `streamRawPredict`

The following partner models support labels.

- [Anthropic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude)
- [Mistral AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/mistral)

Labels are only forwarded to Cloud Billing when the request uses the [PayGo](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) consumption option. Requests using the [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput/overview) consumption option will silently ignore labels sent in the request.

## Supported models for header labels

Header labels are written only to the inference request metadata log, so they work on the models and methods that the log records.

- Gemini models: `generateContent` and `streamGenerateContent` .
- Claude models: `rawPredict` and `streamRawPredict` .
- Consumption options: Provisioned Throughput and every pay-as-you-go option that the model offers.
- Other partner models, including Mistral AI, aren't supported. A request to them with header labels still succeeds, but no log entry is written, so the labels aren't recorded anywhere.
- Header labels never reach Cloud Billing. To break down billed charges, use request labels.

## Add a request label to a Google model API call

To add a label to a `generateContent` or `streamGenerateContent` API call, do the following:

### REST

Before using any of the request data, make the following replacements:

- `GENERATE_RESPONSE_METHOD` : The type of response that you want the model to generate. Choose a method that generates how you want the model's response to be returned:
  - `streamGenerateContent` : The response is streamed as it's being generated to reduce the perception of latency to a human audience.
  - `generateContent` : The response is returned after it's fully generated.

- `LOCATION` : The region to process the request.

- `PROJECT_ID` : Your [project ID](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#identifiers) . .

- `MODEL_ID` : The model ID of the model that you want to use.

- `ROLE` : The role in a conversation associated with the content. Specifying a role is required even in singleturn use cases. Acceptable values include the following:
  - `USER` : Specifies content that's sent by you.
  - `MODEL` : Specifies the model's response.

- ```
  PROMPT_TEXT
  ```

  The text instructions to include in the prompt. JSON

- `LABEL_KEY` : The label metadata that you want to associate with this API call.

- `LABEL_VALUE` : The value of the label.

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "contents": {
    "role": "ROLE",
    "parts": { "text": "PROMPT_TEXT" }
  },
  "labels": {
    "LABEL_KEY": "LABEL_VALUE"
  },
}
EOF
```

Then execute the following command to send your REST request:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATE_RESPONSE_METHOD"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
@'
{
  "contents": {
    "role": "ROLE",
    "parts": { "text": "PROMPT_TEXT" }
  },
  "labels": {
    "LABEL_KEY": "LABEL_VALUE"
  },
}
'@  | Out-File -FilePath request.json -Encoding utf8
```

Then execute the following command to send your REST request:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://LOCATION-aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/LOCATION/publishers/google/models/MODEL_ID:GENERATE_RESPONSE_METHOD" | Select-Object -Expand Content
```

You should receive a JSON response similar to the following.

#### Response

```
{
  "candidates": [
    {
      "content": {
        "role": "model",
        "parts": [
          {
            "text": Generative AI is a type of artificial intelligence (AI) that can **create new
            content**, like text, images, audio, video, and even code.
          }
        ]
      },
      "finishReason": "STOP",
      "safetyRatings": [
        {
          "category": "HARM_CATEGORY_HATE_SPEECH",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.037841797,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.06347656
        },
        {
          "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.053466797,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.08496094
        },
        {
          "category": "HARM_CATEGORY_HARASSMENT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.08154297,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.033203125
        },
        {
          "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
          "probability": "NEGLIGIBLE",
          "probabilityScore": 0.071777344,
          "severity": "HARM_SEVERITY_NEGLIGIBLE",
          "severityScore": 0.083984375
        }
      ],
      "avgLogprobs": -0.40486351219383448
    }
  ],
  "usageMetadata": {
    "promptTokenCount": 5,
    "candidatesTokenCount": 555,
    "totalTokenCount": 560
  }
}
```

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

```python
import os

from google import genai

PROJECT_ID = os.getenv("GOOGLE_CLOUD_PROJECT")
LOCATION = os.getenv("LOCATION_ID")
GEMINI_MODEL = os.getenv("GEMINI_MODEL_ID", "gemini-2.5-flash")


def generate_content() -> genai.types.GenerateContentResponse:

    genai_client = genai.Client(enterprise=True, project=PROJECT_ID, location=LOCATION)

    labels = {
        "environment": "testing",
        "feature": "genai",
        "model": "gemini",
    }

    config = genai.types.GenerateContentConfig(temperature=0.4, labels=labels)

    response = genai_client.models.generate_content(
        model=GEMINI_MODEL, contents="What is Generative AI?", config=config
    )

    print(response.text)
    return response
```

Google Cloud products report usage and cost data to Cloud Billing processes at varying intervals. As a result, you might see a delay between your use of Google Cloud services, and the usage and costs being available to view in Cloud Billing. Typically, your costs are available within a day, but can sometimes take more than 24 hours.

## Add a request label to a partner model API call

> **Note:** The `X-Vertex-AI-Labels` header isn't written to the inference request log. To label Claude requests in the log, send [header labels](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls#add-header-labels) , which appear in `jsonPayload.httpHeaders` .

To add a label to a `rawPredict` or `streamRawPredict` API call, do the following:

### REST

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : Your project ID.
- `MODEL_ID` : The model ID of the model you want to use. For example, `claude-opus-4-6` .

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI. You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "anthropic_version": "vertex-2023-10-16",
  "messages": [
    {
      "role": "user",
      "content": "What is Generative AI?"
    }
  ],
  "max_tokens": 1024,
  "stream": false
}
EOF
```

Then execute the following command to send your REST request:

```
REQUEST_LABELS=$(echo -n '{"team": "research", "component": "frontend"}' | base64 --wrap 0)

curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "X-Vertex-AI-Labels: ${REQUEST_LABELS}" \
  -H "Content-Type: application/json; charset=utf-8" \
  -d @request.json \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:rawPredict"
```

### Python

Before trying this sample, follow the Python setup instructions in the [Agent Platform quickstart using client libraries](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/start/client-libraries) .

To authenticate to Agent Platform, set up Application Default Credentials. For more information, see [Set up authentication for a local development environment](https://docs.cloud.google.com/docs/authentication/set-up-adc-local-dev-environment) .

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : Your project ID.
- `MODEL_ID` : The model ID of the model you want to use. For example, `claude-opus-4-6` .

```
import base64
import json

from google.cloud.aiplatform import aiplatform_v1
from google.api import httpbody_pb2

project_id = "PROJECT_ID"
model_id = "MODEL_ID"
request_body = {
    "anthropic_version": "vertex-2023-10-16",
    "messages": [{
        "role": "user",
        "content": [{"type": "text", "text": "What is Generative AI?"}]
    }],
    "max_tokens": 256,
    "stream": True,
}

# Encode labels to base64 for the X-Vertex-AI-Labels header
labels = {
    "team": "research",
    "component": "frontend",
    "environment": "production",
}
labels_json = json.dumps(labels).encode("utf-8")
vertex_header_value = base64.b64encode(labels_json)

endpoint_id=f"projects/{project_id}/locations/global/publishers/anthropic/models/{model_id}"
client = aiplatform_v1.PredictionServiceClient()
responses = client.stream_raw_predict(
    request=aiplatform_v1.StreamRawPredictRequest(
        endpoint=endpoint_id,
        http_body=httpbody_pb2.HttpBody(
            data=json.dumps(request_body).encode("utf-8"),
            content_type="application/json",
        ),
    ),
    metadata=[("x-vertex-ai-labels", vertex_header_value)],
)

for response in responses:
  print(response.data.decode("utf-8"))
```

## Add header labels to API calls

Header labels need no request body changes. Add one `x-goog-agent-platform-observability-label-KEY` header per label to any supported request. The following examples show the request and the resulting fields of the inference request metadata log entry, from test requests on 2026-10-14.

### Add header labels to a Gemini model API call

Send header labels with `generateContent` or `streamGenerateContent` . Replace `PROJECT_ID` with your project ID.

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  -H "x-goog-agent-platform-observability-label-team: payments" \
  -H "x-goog-agent-platform-observability-label-application: invoice-ocr" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/google/models/gemini-2.5-flash:generateContent" \
  -d '{"contents": [{"role": "user", "parts": [{"text": "What is Generative AI?"}]}]}'
```

The log entry records each label under `jsonPayload.httpHeaders` . Header labels are recorded on Provisioned Throughput traffic too, which request labels don't support:

```
{
  "method": "GENERATE_CONTENT",
  "trafficType": "PROVISIONED_THROUGHPUT",
  "httpHeaders": {
    "x-goog-agent-platform-observability-label-application": {"values": ["invoice-ocr"]},
    "x-goog-agent-platform-observability-label-team": {"values": ["payments"]}
  },
  "generateContentDetails": {"usageMetadata": {"promptTokenCount": 6, "candidatesTokenCount": 1, "totalTokenCount": 7}},
  "provisionedThroughput": {"accountingResource": "projects/PROJECT_NUMBER", "ptChargedInputTokenCount": "6", "ptChargedOutputTokenCount": "9"}
}
```

### Add header labels to a Claude model API call

Send header labels with `rawPredict` or `streamRawPredict` . Replace `PROJECT_ID` and `MODEL_ID` , for example `claude-opus-4-6` .

```
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  -H "x-goog-agent-platform-observability-label-team: payments" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL_ID:rawPredict" \
  -d '{"anthropic_version": "vertex-2023-10-16", "messages": [{"role": "user", "content": "What is Generative AI?"}], "max_tokens": 256}'
```

The log entry records the label under `jsonPayload.httpHeaders` , next to Claude's token counts:

```
{
  "method": "RAW_PREDICT",
  "trafficType": "ON_DEMAND",
  "httpHeaders": {
    "x-goog-agent-platform-observability-label-team": {"values": ["payments"]}
  },
  "rawPredictDetails": {"usageMetadata": {"input_tokens": 17, "output_tokens": 16, "cache_read_input_tokens": 0, "cache_creation_input_tokens": 0}}
}
```

A Claude request can also carry request labels in the `X-Vertex-AI-Labels` header, as shown in [Add a request label to a partner model API call](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/add-labels-to-api-calls#add_a_label_to_a_partner_model_api_call) . Those reach Cloud Billing but aren't written to the log entry.

### Query header labels

In Logs Explorer, filter on one header label value:

```
jsonPayload.httpHeaders."x-goog-agent-platform-observability-label-team".values="payments"
```

In Observability Analytics, group by a header label with the [Usage by custom header label](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging#query-labels) query on the [Log inference request metadata](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/inference-metadata-logging) page.
