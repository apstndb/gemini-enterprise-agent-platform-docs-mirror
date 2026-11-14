---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta
title: Muse models from Meta
description: Explore Muse models from Meta in Model Garden on Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

> **Note:** Meta models are not a Google product, and their availability in Gemini Enterprise Agent Platform is subject to the terms for "Separate Offerings" in the AI/ML Services section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms) , and separate terms found in the relevant model card.

Muse models from Meta are available for use as managed APIs on Agent Platform. You can stream your responses to reduce the end-user latency perception. A streamed response uses *server-sent events* (SSE) to incrementally stream the response.

## Managed Meta models

The following models are available from Meta to use in Agent Platform. To find and enable a Meta model, go to its model card in [Model Garden](https://console.cloud.google.com/agent-platform/model-garden) .

### Muse Wonder from Meta

[Muse Wonder from Meta](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-wonder-1-0) is a high-capability reasoning model built for complex software engineering and long-horizon agentic work. In multi-step coding, autonomous agent, and computer-use workflows, it plans tasks, delegates to sub-agents, calls tools in parallel, and recovers from errors.

### Muse Ember from Meta

[Muse Ember from Meta](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-ember-1-0) is an efficient reasoning model built for high-volume agent tasks, including tool calls, coding subtasks, routing, extraction, and long-document processing. Pair it with Muse Wonder or Muse Spark 1.3 for multi-step planning and reasoning.

### Muse Spark 1.3 from Meta

[Muse Spark 1.3 from Meta](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/partner-models/meta/muse-spark-1-3) is a reasoning model trained for agentic workflows and competitive coding. It supports built-in tool calling with Model Context Protocol (MCP) support and a 1M-token context window for multi-step tasks.

## Use Meta models

Muse models from Meta are served through the stateless OpenAI-compatible [Responses API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.publishers.v1.responses) on the `global` endpoint. Chat completions and stateful response storage ( `store: true` ) aren't supported. Send `POST` requests to `https://aiplatform.googleapis.com/v1/projects/ `` PROJECT_ID `` /locations/global/publishers/meta/v1/responses` and pass the bare model ID ( `muse-wonder-1.0` , `muse-ember-1.0` , or `muse-spark-1.3` ) in the `model` field.

Keep the following parameter details in mind when sending requests:

- **Inputs:** Text and image inputs are supported. Audio, video, and PDF inputs aren't supported.
- **Reasoning effort:** Set `reasoning.effort` to `minimal` , `low` , `medium` , `high` , or `xhigh` ( `Muse Ember` also supports `max` ). `none` isn't supported.
- **Tool calling:** `tool_choice` supports `auto` only ( `none` , `required` , and named-function choices aren't supported).

The following examples send a prompt request to Muse Wonder on the global endpoint. Replace `PROJECT_ID` with your Google Cloud project ID.

### REST (curl)

```sh
curl -X POST \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/publishers/meta/v1/responses" \
  -d '{
    "model": "muse-wonder-1.0",
    "reasoning": {"effort": "high"},
    "input": "Write a Python binary search function with type annotations.",
    "max_output_tokens": 4096,
    "stream": false
  }'
```

### Python (OpenAI SDK)

Install the `openai` and `google-auth` libraries ( `pip install --upgrade openai google-auth` ), set up [Application Default Credentials](https://docs.cloud.google.com/docs/authentication/provide-credentials-adc#local-dev) ( `gcloud auth application-default login` ), and then send a request:

```python
import google.auth
import google.auth.transport.requests
from openai import OpenAI

PROJECT_ID = "PROJECT_ID"
LOCATION = "global"

credentials, _ = google.auth.default(
    scopes=["https://www.googleapis.com/auth/cloud-platform"]
)
credentials.refresh(google.auth.transport.requests.Request())

client = OpenAI(
    base_url=f"https://aiplatform.googleapis.com/v1/projects/{PROJECT_ID}/locations/{LOCATION}/publishers/meta/v1",
    api_key=credentials.token,
)

response = client.responses.create(
    model="muse-wonder-1.0",
    reasoning={"effort": "high"},
    input="Write a Python binary search function with type annotations.",
    max_output_tokens=4096,
)
print(response.output_text)
```
