---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode
title: Fast mode with Anthropic Claude models
description: 'Use fast mode (speed: fast) with supported Anthropic Claude models on Gemini Enterprise Agent Platform to accelerate output token generation for latency-sensitive agentic workflows.'
data_source: docs.cloud.google.com
---

Fast mode accelerates output token generation for supported Anthropic Claude models on Gemini Enterprise Agent Platform. It uses a high-speed serving configuration that preserves the intelligence and safety capabilities of the base model. You enable fast mode on online prediction requests by setting `"speed": "fast"` in the request body.

Use fast mode for latency-sensitive, interactive workloads where waiting on token generation interrupts developer or user flow:

- **Interactive agentic coding** : Iterate on multi-step coding, refactoring, and debugging tasks with human-in-the-loop agents without context switching.
- **Live planning** : Gather repository or operational context and generate execution plans interactively.
- **Incident response** : Triage production alerts and synthesize remediation steps when inference turnaround time is critical.

## Supported models and lifecycle policy

Fast mode is offered on the latest version of a supported Claude model family and during a 30-day transition window on the retiring version. Agent Platform supports fast mode for the following models:

- [Anthropic's Claude Fable 5.2 on Google Cloud](https://console.cloud.google.com/agent-platform/publishers/anthropic/model-garden/claude-fable-5-2) ( `claude-fable-5-2` )

When a new version of a supported model family launches, fast mode on the previous version in that family is retired **30 days** after the new version launches. After the 30-day retirement window closes, requests to the previous model version that include `"speed": "fast"` return an `HTTP 400` ( `INVALID_ARGUMENT` ) error. Standard-speed requests to that model version continue to work normally. To continue using fast mode, update your requests to target the latest model version or remove `"speed": "fast"` from the request body.

## Supported locations

Fast mode is available at the following API location IDs for supported models:

- **Global (Anthropic's Claude Fable 5.2 on Google Cloud)** : `global`
- **United States multi-region (Anthropic's Claude Fable 5.2 on Google Cloud)** : `us`
- **Europe multi-region (Anthropic's Claude Fable 5.2 on Google Cloud)** : `eu`

Direct regional endpoints aren't publicly supported for fast mode. Sending a request with `"speed": "fast"` to a location where fast mode isn't available returns an `HTTP 400` ( `FAILED_PRECONDITION` ) error.

## Before you begin

Before sending fast mode requests, complete the following setup steps. Fast mode uses the same project setup and Model Garden enablement as standard Claude requests. For additional partner model setup details, see [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude#before-you-begin) .

1.  Go to one of the following Model Garden model cards, click **Enable** , and complete any model-specific terms or data-sharing requirements:
    - 

### Required roles

To get the permissions that you need to send fast mode prediction requests to Claude models, ask your administrator to grant you the following IAM roles on your Google Cloud project:

- Send prediction requests to partner models: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Send a fast mode request

To use fast mode, send a request to the standard publisher model endpoint (for example, `claude-fable-5-2` ) and set `"speed": "fast"` in the top-level request body. No `anthropic-beta` header is required, and there is no separate model card to enable in Model Garden.

### REST

The following sample sends a prediction request to `claude-fable-5-2` on the `global` endpoint with `"speed": "fast"` enabled.

Before using any of the request data, make the following replacements:

- ` PROJECT_ID ` : Your Google Cloud project ID (for example, `my-agent-project` ).
- ` MODEL ` : A [Claude model that supports fast mode](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-models) , such as `claude-fable-5-2` (default: `claude-fable-5-2` ). Always specify the base model ID in the endpoint URL.

This sample uses the `global` endpoint. To use a [supported multi-region endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-locations) instead, see [Specify the multi-region endpoint](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/use-partner-models#multi-region) .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL:rawPredict
```

Request JSON body:

```
{
  "anthropic_version": "vertex-2023-10-16",
  "speed": "fast",
  "max_tokens": 1024,
  "messages": [
    {
      "role": "user",
      "content": "Analyze the root cause of an HTTP 502 spike on an upstream GKE ingress controller and list three immediate mitigation steps."
    }
  ]
}
```

To send your request, choose one of these options:

#### curl

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL:rawPredict"
```

#### PowerShell

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` , and execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -ContentType: "application/json; charset=utf-8" `
    -InFile request.json `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/anthropic/models/MODEL:rawPredict" | Select-Object -Expand Content
```

The response is a JSON object similar to the following. When the request is served in fast mode, the `usage` object includes `"speed": "fast"` .

#### Response

```
{
  "id": "msg_vrtx_01FastModeExample89ABcdEF",
  "type": "message",
  "role": "assistant",
  "model": "claude-fable-5-2",
  "content": [
    {
      "type": "text",
      "text": "Here are the most common root causes for an HTTP 502 spike on a GKE Ingress controller and three immediate mitigation steps..."
    }
  ],
  "stop_reason": "end_turn",
  "stop_sequence": null,
  "usage": {
    "input_tokens": 34,
    "output_tokens": 218,
    "speed": "fast"
  }
}
```

### Python

Using the Anthropic Vertex SDK ( `anthropic[vertex]` ), pass `extra_body={"speed": "fast"}` when calling `client.messages.create()` :

```
from anthropic import AnthropicVertex
from anthropic.types import Message


def generate_with_fast_mode(
    project_id: str = "PROJECT_ID",
) -> Message:
    client = AnthropicVertex(
        project_id=project_id,
        region="global",
    )

    message = client.messages.create(
        model="claude-fable-5-2",
        max_tokens=1024,
        extra_body={"speed": "fast"},
        messages=[
            {
                "role": "user",
                "content": (
                    "Analyze the root cause of an HTTP 502 spike on an upstream "
                    "GKE ingress controller and list three immediate mitigation "
                    "steps."
                ),
            }
        ],
    )
    print(message.model_dump_json(indent=2))
    return message
```

### Check which speed was used

You can verify that a request was served in fast mode by inspecting the `usage.speed` field in the response:

- **Fast mode** : `usage.speed` is present and set to `"fast"` (in unary responses, or in the `message_start` or `message_delta` events for streaming responses).
- **Standard speed** : When you send a standard request ( `"speed": "standard"` or `speed` omitted), `usage.speed` is either `"standard"` or omitted.

## Quotas, monitoring, and access control

Fast mode uses dedicated capacity and rate limits that are isolated from standard-speed traffic, while inheriting your project's access configuration for the base model.

### Quotas

On global and multi-region endpoints, fast mode requests consume a dedicated [shared lineage quota](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas#shared-lineage-quotas) bucket separate from standard-speed model quota. Fast-mode traffic doesn't draw from your standard `anthropic-claude-fable` quota, and standard-speed traffic doesn't draw from your fast-mode quota.

To view or request a fast mode quota increase on the [Quotas and system limits](https://console.cloud.google.com/iam-admin/quotas) page in the Google Cloud console, filter by `base_model` :

- `anthropic-claude-fable-fast` (applies to global and multi-region endpoints)

### Consumption options and Provisioned Throughput

Fast mode doesn't support [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) :

- **PayGo only** : Fast mode requests always use [pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) , even if your project has an active Provisioned Throughput order for the base model. Fast-mode traffic never consumes or spills over from a Provisioned Throughput order.
- **`dedicated` request headers are throttled** : Don't include the `X-Vertex-AI-LLM-Request-Type: dedicated` HTTP header (or gRPC metadata) on fast mode requests. Fast mode doesn't have Provisioned Throughput quota, and `dedicated` requests can't spill over to pay-as-you-go. As a result, fast mode requests with `X-Vertex-AI-LLM-Request-Type: dedicated` return an `HTTP 429` ( `RESOURCE_EXHAUSTED` ) error. Omit the header or set `X-Vertex-AI-LLM-Request-Type: shared` instead.

### Monitor fast mode metrics

In Cloud Monitoring, fast mode traffic reports `model_user_id="claude-fable-5-2-fast"` rather than the base model ID ( `claude-fable-5-2` ). Filter by `model_user_id="claude-fable-5-2-fast"` in Metrics Explorer to monitor request counts, token usage, and latency for fast mode separately from standard-speed traffic.

> **Caution:** `claude-fable-5-2-fast` is a monitoring metric label only, not a callable model ID. Always send API requests to the base model ID (such as `claude-fable-5-2` ) with `"speed": "fast"` in the request body. Calling `claude-fable-5-2-fast` in the endpoint URL returns an `HTTP 404` ( `NOT_FOUND` ) error.

### Access control and organization policy

Fast mode uses the same [required roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#required-roles) and Model Garden enablement state as the base model. If a request returns `403 PERMISSION_DENIED` , verify that your principal has the Agent Platform User role ( `roles/aiplatform.user` ) and that the base model is enabled in Model Garden.

If your organization enforces the `constraints/vertexai.allowedModels` organization policy constraint, fast mode is governed by the base model's `:predict` value (for example, `publishers/anthropic/models/claude-fable-5-2:predict` ):

- Allowing `publishers/anthropic/models/claude-fable-5-2:predict` allows both standard-speed and fast-mode requests to `claude-fable-5-2` .
- Denying `publishers/anthropic/models/claude-fable-5-2:predict` blocks both standard-speed and fast-mode requests.

For more information about organization policies, see [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access) .

## Pricing

Fast mode always uses [pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) billing and has separate pricing from standard-speed requests:

- **Tokens** : Priced at **2x the standard-speed token rates** across all token types (input, output, 5-minute and 1-hour cache write, and cache hit tokens).
- **Web search** : [Web search](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/web-search) tool calls are billed at the **standard (1x) rate** .

Usage is billed under the base model's Google Cloud SKU with a fast-mode label. For regional and global token rates, see the [Agent Platform pricing page](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing#partner-models) .

## Limitations and error handling

Keep the following limitations in mind when using fast mode:

- **No Provisioned Throughput** : Fast mode doesn't support [Provisioned Throughput](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/provisioned-throughput) and always uses pay-as-you-go. Sending a fast mode request with the `X-Vertex-AI-LLM-Request-Type: dedicated` header returns an `HTTP 429` ( `RESOURCE_EXHAUSTED` ) error.
- **No batch predictions** : Fast mode is designed for interactive, real-time inference and isn't supported with [batch predictions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/batch) .
- **Prompt cache isolation** : [Prompt caches](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching) aren't shared between standard-speed and fast-mode requests. A cache entry written at standard speed won't produce a cache hit in fast mode. Similarly, a fast-mode cache entry won't produce a cache hit at standard speed.
- **No silent downgrade** : If a request with `"speed": "fast"` can't be served in fast mode, Agent Platform returns an error instead of falling back to standard speed.

The following table summarizes the errors returned for invalid or unsupported fast mode requests:

| HTTP status and code      | Error message                                              | Cause and remediation                                                                                                                                                                                                                                                                                 |
|---------------------------|------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `400 INVALID_ARGUMENT`    | `Fast mode (speed: fast) is not supported for this model.` | The target model doesn't offer fast mode, or its fast mode was retired 30 days after a newer model version launched. Target a [supported model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-models) or remove `"speed": "fast"` . |
| `400 INVALID_ARGUMENT`    | `Invalid value for speed; expected "standard" or "fast".`  | The `speed` field contains an unsupported value or isn't a string. Specify `"fast"` or `"standard"` .                                                                                                                                                                                                 |
| `400 INVALID_ARGUMENT`    | `Invalid request body: duplicate keys or malformed JSON.`  | The JSON request body contains duplicate keys (such as duplicate `"speed"` keys) or malformed JSON syntax. Send valid JSON with a single `"speed"` key.                                                                                                                                               |
| `400 INVALID_ARGUMENT`    | `Fast mode is not supported for batch prediction.`         | The request was submitted to a batch prediction job with `"speed": "fast"` . Remove `"speed": "fast"` for batch workloads.                                                                                                                                                                            |
| `400 FAILED_PRECONDITION` | `Fast mode is not available in this location.`             | Fast mode isn't deployed in the requested region. Route the request to one of the [supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-locations) .                                                                  |
| `404 NOT_FOUND`           | `Publisher Model ... was not found`                        | The request URL targeted the monitoring metric label ( `claude-fable-5-2-fast` ) instead of a callable model ID. Target the base model ID ( `claude-fable-5-2` ) and pass `"speed": "fast"` in the request body.                                                                                      |
| `429 RESOURCE_EXHAUSTED`  | `Too many requests. Exceeded the provisioned throughput`   | The request included both `"speed": "fast"` and the `X-Vertex-AI-LLM-Request-Type: dedicated` header. Fast mode doesn't support Provisioned Throughput and always uses pay-as-you-go; remove `X-Vertex-AI-LLM-Request-Type: dedicated` (or set it to `shared` ).                                      |
| `429 RESOURCE_EXHAUSTED`  | Quota exceeded for `anthropic-claude-fable-fast`           | Your project exceeded its fast mode QPM, input TPM, or output TPM quota in that location. Retry with exponential backoff or request a quota increase for `anthropic-claude-fable-fast` .                                                                                                              |

## Handle fast mode errors

Because Agent Platform doesn't silently downgrade fast mode requests, your application decides what happens when fast mode isn't available. For example, fast mode is [retired 30 days after the next version launches](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-models) , or a location might not offer fast mode. The following Python samples match the specific fast mode error messages so unrelated `HTTP 400` errors still surface.

### Fall back to standard speed

For workloads that can tolerate higher latency, catch the fast mode availability errors and retry the request at standard speed:

```
import anthropic
from anthropic import AnthropicVertex
from anthropic.types import Message

# Errors that mean fast mode isn't available for this model or location.
_FAST_MODE_UNAVAILABLE = (
    "Fast mode (speed: fast) is not supported for this model.",
    "Fast mode is not available in this location.",
)


def generate_with_standard_fallback(
    project_id: str = "PROJECT_ID",
    region: str = "LOCATION",
    model: str = "claude-fable-5-2",
) -> Message:
    client = AnthropicVertex(project_id=project_id, region=region)
    messages = [{"role": "user", "content": "PROMPT"}]
    try:
        return client.messages.create(
            model=model,
            max_tokens=1024,
            messages=messages,
            extra_body={"speed": "fast"},
        )
    except anthropic.BadRequestError as e:
        if not any(msg in str(e) for msg in _FAST_MODE_UNAVAILABLE):
            raise
        # Fast mode isn't available: retry at standard speed.
        return client.messages.create(
            model=model,
            max_tokens=1024,
            messages=messages,
        )
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .
- `LOCATION` : a [supported location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-locations) , such as `global` (default: `global` ).
- `PROMPT` : the prompt text to send to the model.

### Move to the next model version

To keep fast mode after retirement on your model version, retry the request with fast mode on the next version:

```
import anthropic
from anthropic import AnthropicVertex
from anthropic.types import Message

_FAST_MODE_NOT_SUPPORTED = (
    "Fast mode (speed: fast) is not supported for this model."
)


def generate_with_next_version(
    project_id: str = "PROJECT_ID",
    region: str = "LOCATION",
    model: str = "CURRENT_MODEL",
    next_model: str = "NEXT_MODEL",
) -> Message:
    client = AnthropicVertex(project_id=project_id, region=region)
    messages = [{"role": "user", "content": "PROMPT"}]
    try:
        return client.messages.create(
            model=model,
            max_tokens=1024,
            messages=messages,
            extra_body={"speed": "fast"},
        )
    except anthropic.BadRequestError as e:
        if _FAST_MODE_NOT_SUPPORTED not in str(e):
            raise
        # Fast mode is retired on this version: use the next version.
        return client.messages.create(
            model=next_model,
            max_tokens=1024,
            messages=messages,
            extra_body={"speed": "fast"},
        )
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .
- `LOCATION` : a [supported location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-locations) , such as `global` (default: `global` ).
- `CURRENT_MODEL` and `NEXT_MODEL` : the model version you use (such as `claude-fable-5-2` ) and the next version in the same model family.
- `PROMPT` : the prompt text to send to the model.

The next-version pattern handles only the model retirement error. If the location doesn't offer fast mode, the next version won't resolve the error. Route the request to a [supported location](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/fast-mode#supported-locations) instead.

## What's next

- [Request predictions with Claude models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/use-claude)
- [Quotas for Anthropic Claude models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/quotas)
- [Prompt caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/claude/prompt-caching)
- [Control access to Model Garden models](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/control-model-access)
