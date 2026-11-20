---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier
title: Use the Deferred tier
description: Run asynchronous, multi-turn Gemini model calls at a discounted rate on Gemini Enterprise Agent Platform by using the Deferred tier in the Interactions API.
data_source: docs.cloud.google.com
---

Use the Deferred tier to run asynchronous, multi-turn Gemini model calls for custom agents at a [discounted rate](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#pricing) on Gemini Enterprise Agent Platform. On the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) , Agent Platform queues each deferred turn for background execution within a 24-hour target and retains state for 7 days.

The Deferred tier fits latency-tolerant agentic workloads that need per-turn control, such as the following:

- **Multi-step coding and security agents** : Repository vulnerability scans, automated code migrations, and regression triage.
- **Document and research pipelines** : Technical design reviews, financial backtesting, and multi-document synthesis with tool calling.
- **Offline agent evaluations** : Large-scale quality benchmarks that chain `previous_interaction_id` turns without real-time latency constraints.

To compare all compute models, see [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) . To schedule Agent Development Kit (ADK) agents or managed runs on the Gemini Deep Research Agent, see [Autonomous agent scheduling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling) .

## Supported models and locations

The Deferred tier is supported exclusively on the `global` endpoint ( `locations/global` on `aiplatform.googleapis.com` ). Sending a request with `service_tier="deferred"` to a regional endpoint or to the `us` or `eu` multi-region endpoints returns HTTP `400` ( `"code": "invalid_request"` ).

The following mainline Gemini models support the Deferred tier on the `global` endpoint:

- [Gemini 4 Carbon ( `gemini-4-carbon` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon)
- [Gemini 4 Argon ( `gemini-4-argon` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon)
- [Gemini 3.8 Flash ( `gemini-3.8-flash` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-8-flash)
- [Gemini 3.7 Flash ( `gemini-3.7-flash` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-7-flash)
- [Gemini 3.6 Flash ( `gemini-3.6-flash` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-6-flash)
- [Gemini 3.5 Flash-Lite ( `gemini-3.5-flash-lite` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash-lite)
- [Gemini 3.5 Flash ( `gemini-3.5-flash` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
- [Gemini 3.1 Flash-Lite ( `gemini-3.1-flash-lite` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-flash-lite)
- [Gemini 3.1 Pro ( `gemini-3.1-pro-preview` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro)

If your project has allowlist access through your Google Cloud account team, you can also use the following Cyber models:

- [Gemini 4 Carbon for cyber ( `gemini-4-carbon-cyber-permissive` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-carbon#cyber)
- [Gemini 4 Argon Cyber Permissive ( `gemini-4-argon-cyber-permissive` )](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/4-argon#cyber)

## Before you begin

In an existing billing-enabled Google Cloud project, complete the following prerequisite setup steps:

### Required roles

To get the permissions that you need to create, monitor, and cancel deferred model calls, ask your administrator to grant you the following IAM roles on your Google Cloud project:

- Create, poll, cancel, and delete deferred interactions: [Agent Platform User](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.user) ( `roles/aiplatform.user` )
- Monitor deferred interactions (read-only): [Agent Platform Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/aiplatform#aiplatform.viewer) ( `roles/aiplatform.viewer` )
- Read multimodal input files from Cloud Storage (optional): [Storage Object Viewer](https://docs.cloud.google.com/iam/docs/roles-permissions/storage#storage.objectViewer) ( `roles/storage.objectViewer` )

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

### Install the Google Gen AI SDK

If you use a client library, install or upgrade the Google Gen AI SDK ( `@google/genai >= 2.32.0` or `google-genai >= 2.34.0` ) in your development environment:

### Node.js

```
npm install @google/genai@latest
```

### Python

```
pip install --upgrade "google-genai>=2.34.0"
```

## Create and manage deferred model calls

Run the following procedures in the environment that you set up in [Before you begin](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#before-you-begin) . The REST samples authenticate with your gcloud CLI credentials, and the Google Gen AI SDK samples use Application Default Credentials (ADC). If a call returns an error, see [Troubleshoot](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#troubleshoot) .

### Create a deferred model call

Submit an asynchronous turn by calling `interactions.create` with `service_tier="deferred"` , `background=true` , and `store=true` . Omit `stream` or set it to `false` . Before you run a sample, replace `PROJECT_ID` with your Google Cloud project ID, such as `my-agent-project` .

### REST

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
{
  "model": "gemini-4-argon",
  "input": "In two sentences, explain how a circuit breaker differs from exponential backoff in a distributed microservice architecture.",
  "service_tier": "deferred",
  "background": true,
  "store": true
}
```

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "model": "gemini-4-argon",
  "input": "In two sentences, explain how a circuit breaker differs from exponential backoff in a distributed microservice architecture.",
  "service_tier": "deferred",
  "background": true,
  "store": true
}
EOF
```

Then execute the following command to send your REST request:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
@'
{
  "model": "gemini-4-argon",
  "input": "In two sentences, explain how a circuit breaker differs from exponential backoff in a distributed microservice architecture.",
  "service_tier": "deferred",
  "background": true,
  "store": true
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
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response returns a JSON payload similar to the following:

```
{
  "id": "v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0",
  "model": "gemini-4-argon",
  "status": "queued",
  "service_tier": "deferred",
  "steps": []
}
```

### Node.js

```
import { GoogleGenAI } from "@google/genai";

async function createDeferredInteraction(projectId) {
  const ai = new GoogleGenAI({
    enterprise: true,
    project: projectId,
    location: "global",
  });

  const interaction = await ai.interactions.create({
    model: "gemini-4-argon",
    input:
      "In two sentences, explain how a circuit breaker differs from exponential backoff in a distributed microservice architecture.",
    service_tier: "deferred",
    background: true,
    store: true,
  });

  console.log(`Interaction ID: ${interaction.id}`);
  console.log(`Status: ${interaction.status}`);
  console.log(`Service tier: ${interaction.service_tier}`);
  return interaction.id ?? "";
}

await createDeferredInteraction("PROJECT_ID");
```

The output is similar to the following:

```
Interaction ID: v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0
Status: queued
Service tier: deferred
```

### Python

```
from google import genai

def create_deferred_interaction(project_id: str) -> str:
    client = genai.Client(
        enterprise=True,
        project=project_id,
        location="global",
    )

    interaction = client.interactions.create(
        model="gemini-4-argon",
        input=(
            "In two sentences, explain how a circuit breaker differs from "
            "exponential backoff in a distributed microservice architecture."
        ),
        service_tier="deferred",
        background=True,
        store=True,
    )

    print(f"Interaction ID: {interaction.id}")
    print(f"Status: {interaction.status}")
    print(f"Service tier: {interaction.service_tier}")
    return interaction.id or ""

create_deferred_interaction("PROJECT_ID")
```

The output is similar to the following:

```
Interaction ID: v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0
Status: queued
Service tier: deferred
```

### Poll status and retrieve token usage

Poll `interactions.get` with backoff while `status` is `queued` or `in_progress` . When the turn reaches a final status, read `output_text` and `usage` .

The Deferred tier targets completing 95% of turns within 24 hours without a credit-backed latency SLA. The following table describes the `status` values of an `Interaction` resource:

| Status                  | Final | Meaning and next step                                                                                                                                                                       |
|-------------------------|-------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `queued`                | No    | Accepted and waiting for capacity. Poll `interactions.get` with backoff. Don't request `stream=true` yet.                                                                                   |
| `in_progress`           | No    | Running. Continue to poll `interactions.get` , or attach an SSE stream with `stream=true` .                                                                                                 |
| `requires_action`       | Yes   | The turn ended on a model-emitted `function_call` step. Run the tool, and then create a new turn with `previous_interaction_id` .                                                           |
| `requires_continuation` | Yes   | A long-decode turn stopped with partial output and a `continuation_token` . Resume with `previous_interaction_id` and `continuation_token` , omit `input` , and raise `max_output_tokens` . |
| `completed`             | Yes   | The turn finished. Read `output_text` and `usage` , or pass `id` as `previous_interaction_id` on the next turn.                                                                             |
| `incomplete`            | Yes   | The turn stopped early, such as when it reached `max_output_tokens` . Inspect the partial `steps` and `usage` .                                                                             |
| `failed`                | Yes   | The turn hit a runtime error or exceeded the 24-hour completion window. The API doesn't use an `expired` status. Inspect `error` , and then submit a new request.                           |
| `cancelled`             | Yes   | A call to `interactions.cancel` stopped the turn before it finished.                                                                                                                        |

If a long-decode turn ends as `requires_continuation` , resume it by calling `interactions.create` with `previous_interaction_id` , `continuation_token` , `background=true` , `store=true` , and `service_tier="deferred"` . Omit `input` and set `max_output_tokens` higher than the tokens generated so far. To learn how each final status is billed, see [Pricing and billing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#pricing) .

Before you run a sample, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .

- `INTERACTION_ID` : the interaction ID returned when you created the deferred model call, such as `v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0` .

### REST

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .
- `INTERACTION_ID` : the interaction ID returned when you created the deferred model call, such as `v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0` .

HTTP method and URL:

```
GET https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID
```

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X GET \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID"
```

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method GET `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID" | Select-Object -Expand Content
```

The response returns a JSON payload similar to the following:

```
{
  "id": "v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0",
  "model": "gemini-4-argon",
  "status": "completed",
  "service_tier": "deferred",
  "steps": [
    {
      "type": "model_output",
      "content": [
        {
          "type": "text",
          "text": "Exponential backoff increases the wait time between retries to give a struggling service time to recover. A circuit breaker stops sending requests once failures pass a threshold, failing fast until the downstream service is healthy again."
        }
      ]
    }
  ],
  "usage": {
    "total_input_tokens": 27,
    "total_output_tokens": 41,
    "total_tokens": 68
  }
}
```

### Node.js

```
import { GoogleGenAI } from "@google/genai";

const PENDING_STATES = new Set(["queued", "in_progress"]);
const MAX_DELAY_MS = 30000;
const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

async function waitForDeferredInteraction(projectId, interactionId) {
  const ai = new GoogleGenAI({
    enterprise: true,
    project: projectId,
    location: "global",
  });

  let delayMs = 5000;
  let current = await ai.interactions.get(interactionId);

  while (PENDING_STATES.has(current.status)) {
    await sleep(delayMs);
    delayMs = Math.min(delayMs * 2, MAX_DELAY_MS);
    current = await ai.interactions.get(interactionId);
  }

  console.log(`Status: ${current.status}`);
  if (current.status === "failed") {
    throw new Error(`Deferred turn failed: ${JSON.stringify(current.error)}`);
  }
  if (current.output_text) {
    console.log(current.output_text);
  }
  if (current.usage) {
    console.log(`Input tokens: ${current.usage.total_input_tokens}`);
    console.log(`Output tokens: ${current.usage.total_output_tokens}`);
    console.log(`Total tokens: ${current.usage.total_tokens}`);
  }
  return current.output_text ?? "";
}

await waitForDeferredInteraction(
  "PROJECT_ID",
  "INTERACTION_ID",
);
```

The output is similar to the following:

```
Status: completed
Exponential backoff increases the wait time between retries to give a struggling service time to recover. A circuit breaker stops sending requests once failures pass a threshold, failing fast until the downstream service is healthy again.
Input tokens: 27
Output tokens: 41
Total tokens: 68
```

### Python

```
import time
from google import genai

PENDING_STATES = frozenset({"queued", "in_progress"})
MAX_DELAY_SECONDS = 30.0

def wait_for_deferred_interaction(
    project_id: str,
    interaction_id: str,
) -> str:
    client = genai.Client(
        enterprise=True,
        project=project_id,
        location="global",
    )

    delay_seconds = 5.0
    current = client.interactions.get(interaction_id)

    while current.status in PENDING_STATES:
        time.sleep(delay_seconds)
        delay_seconds = min(delay_seconds * 2.0, MAX_DELAY_SECONDS)
        current = client.interactions.get(interaction_id)

    print(f"Status: {current.status}")
    if current.status == "failed":
        raise RuntimeError(f"Deferred turn failed: {current.error}")
    if current.output_text:
        print(current.output_text)
    if current.usage:
        print(f"Input tokens: {current.usage.total_input_tokens}")
        print(f"Output tokens: {current.usage.total_output_tokens}")
        print(f"Total tokens: {current.usage.total_tokens}")
    return current.output_text or ""

wait_for_deferred_interaction(
    "PROJECT_ID",
    "INTERACTION_ID",
)
```

The output is similar to the following:

```
Status: completed
Exponential backoff increases the wait time between retries to give a struggling service time to recover. A circuit breaker stops sending requests once failures pass a threshold, failing fast until the downstream service is healthy again.
Input tokens: 27
Output tokens: 41
Total tokens: 68
```

### Optional: Stream output while a call runs

After `interactions.get` reports `status="in_progress"` , you can attach a Server-Sent Events (SSE) stream with `stream=true` and resume dropped connections with `last_event_id` :

### REST

Append `?stream=true` to the `interactions.get` URL. When reconnecting, also append `&last_event_id= `` EVENT_ID` , replacing `EVENT_ID` with the last received event ID.

### Node.js

Iterate over `await ai.interactions.get(interactionId, { stream: true, last_event_id: lastEventId })` , record `event.event_id` , and read `event.delta?.text` on `step.delta` events.

### Python

Iterate over `client.interactions.get(interaction_id, stream=True, last_event_id=last_event_id)` , record `event.event_id` , and read `event.delta.text` on `step.delta` events.

For more information about SSE streaming and reconnection, see the [Interactions API developer guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide) .

### Chain multi-turn deferred workflows

Continue a multi-turn conversation or return tool execution results by passing the `id` of a `completed` or `requires_action` interaction in `previous_interaction_id` . Turn-scoped fields such as `tools` , `system_instruction` , and `generation_config` don't carry over automatically, so pass them on each turn that requires them. Chained turns remain eligible for [implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview) , though cached prefixes might expire across multi-hour queue waits. For tool-result step schemas, see the [Interactions API developer guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide) .

Before you run a sample, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .

- `PREVIOUS_INTERACTION_ID` : the ID of the preceding `completed` or `requires_action` turn, such as `v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0` .

### REST

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .
- `PREVIOUS_INTERACTION_ID` : the completed or action-required interaction ID from the preceding turn, such as `v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions
```

Request JSON body:

```
{
  "model": "gemini-4-argon",
  "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
  "input": "Draft a one-paragraph rollout checklist for adding a circuit breaker to a payment gateway client without causing false trips.",
  "service_tier": "deferred",
  "background": true,
  "store": true
}
```

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
cat > request.json << 'EOF'
{
  "model": "gemini-4-argon",
  "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
  "input": "Draft a one-paragraph rollout checklist for adding a circuit breaker to a payment gateway client without causing false trips.",
  "service_tier": "deferred",
  "background": true,
  "store": true
}
EOF
```

Then execute the following command to send your REST request:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d @request.json \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions"
```

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Save the request body in a file named `request.json` . Run the following command in the terminal to create or overwrite this file in the current directory:

```
@'
{
  "model": "gemini-4-argon",
  "previous_interaction_id": "PREVIOUS_INTERACTION_ID",
  "input": "Draft a one-paragraph rollout checklist for adding a circuit breaker to a payment gateway client without causing false trips.",
  "service_tier": "deferred",
  "background": true,
  "store": true
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
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions" | Select-Object -Expand Content
```

The response returns a JSON payload similar to the following:

```
{
  "id": "v1_Ch1Lm9RUXhPNlJqS1lBMk56UjdVOGdnPT0",
  "model": "gemini-4-argon",
  "previous_interaction_id": "v1_ChpJd25XUXhPNlJqS1lBMk56UjdVOGdnPT0",
  "status": "queued",
  "service_tier": "deferred",
  "steps": []
}
```

### Node.js

```
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
  enterprise: true,
  project: "PROJECT_ID",
  location: "global",
});

const followUp = await ai.interactions.create({
  model: "gemini-4-argon",
  previous_interaction_id: "PREVIOUS_INTERACTION_ID",
  input:
    "Draft a one-paragraph rollout checklist for adding a circuit breaker to a payment gateway client without causing false trips.",
  service_tier: "deferred",
  background: true,
  store: true,
});

console.log(`Follow-up ID: ${followUp.id} (${followUp.status})`);
```

The output is similar to the following:

```
Follow-up ID: v1_Ch1Lm9RUXhPNlJqS1lBMk56UjdVOGdnPT0 (queued)
```

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

follow_up = client.interactions.create(
    model="gemini-4-argon",
    previous_interaction_id="PREVIOUS_INTERACTION_ID",
    input=(
        "Draft a one-paragraph rollout checklist for adding a circuit "
        "breaker to a payment gateway client without causing false trips."
    ),
    service_tier="deferred",
    background=True,
    store=True,
)

print(f"Follow-up ID: {follow_up.id} ({follow_up.status})")
```

The output is similar to the following:

```
Follow-up ID: v1_Ch1Lm9RUXhPNlJqS1lBMk56UjdVOGdnPT0 (queued)
```

### Cancel a deferred model call

To stop a deferred interaction whose `status` is `queued` or `in_progress` , call `interactions.cancel` . Calling `interactions.cancel` on an interaction in any other status returns HTTP `409` ( `"code": "aborted"` ). To learn how cancellation affects billing, see [Pricing and billing](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#pricing) .

Before you run a sample, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .

- `INTERACTION_ID` : the ID of a `queued` or `in_progress` interaction, such as `v1_ChpQcTNuWkVrN0xmUjJ4Yk1oVzhkSmc9PQ` .

### REST

Before using any of the request data, make the following replacements:

- `PROJECT_ID` : your Google Cloud project ID, such as `my-agent-project` .
- `INTERACTION_ID` : the ID of a queued or in-progress interaction to cancel, such as `v1_ChpQcTNuWkVrN0xmUjJ4Yk1oVzhkSmc9PQ` .

HTTP method and URL:

```
POST https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID/cancel
```

To send your request, expand one of these options:

#### curl (Linux, macOS, or Cloud Shell)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) , or by using [Cloud Shell](https://docs.cloud.google.com/shell/docs) , which automatically logs you into the `gcloud` CLI . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
curl -X POST \
     -H "Authorization: Bearer $(gcloud auth print-access-token)" \
     -H "Content-Type: application/json; charset=utf-8" \
     -d "" \
     "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID/cancel"
```

#### PowerShell (Windows)

> **Note:** The following command assumes that you have logged in to the `gcloud` CLI with your user account by running [`gcloud init`](https://docs.cloud.google.com/sdk/gcloud/reference/init) or [`gcloud auth login`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/login) . You can check the currently active account by running [`gcloud auth list`](https://docs.cloud.google.com/sdk/gcloud/reference/auth/list) .

Execute the following command:

```
$cred = gcloud auth print-access-token
$headers = @{ "Authorization" = "Bearer $cred" }

Invoke-WebRequest `
    -Method POST `
    -Headers $headers `
    -Uri "https://aiplatform.googleapis.com/v1/projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID/cancel" | Select-Object -Expand Content
```

The response returns a JSON payload similar to the following:

```
{
  "id": "v1_ChpQcTNuWkVrN0xmUjJ4Yk1oVzhkSmc9PQ",
  "model": "gemini-4-argon",
  "status": "cancelled",
  "service_tier": "deferred"
}
```

### Node.js

```
import { GoogleGenAI } from "@google/genai";

const ai = new GoogleGenAI({
  enterprise: true,
  project: "PROJECT_ID",
  location: "global",
});

const cancelled = await ai.interactions.cancel("INTERACTION_ID");
console.log(`Status: ${cancelled.status}`);
```

The output is the following:

```
Status: cancelled
```

### Python

```
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

cancelled = client.interactions.cancel("INTERACTION_ID")
print(f"Status: {cancelled.status}")
```

The output is the following:

```
Status: cancelled
```

## Pricing, quotas, and security controls

Review billing rules, quotas, payload limits, and security controls before you run production workloads on the Deferred tier.

### Pricing and billing

Deferred model calls are billed at a 50% discount compared to [Standard pay-as-you-go](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/standard-paygo) rates for input, output, and thinking tokens. Billing follows these rules:

- **Discount stacking** : The deferred discount stacks with contract discounts and [implicit context caching](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/context-cache/context-cache-overview) token discounts, applying on top of the cached rate.
- **No fallback to standard rates** : Deferred requests never spill over or downgrade to Standard PayGo, so they aren't billed at undiscounted on-demand rates.
- **Billing by model call** : Each model call that a turn makes is billed. Turns that end as `completed` , `incomplete` , `requires_action` , or `requires_continuation` are billed at the deferred rate.
- **Cancelled turns** : A turn that you cancel while it's `queued` isn't billed. If you cancel a turn while it's `in_progress` , model calls that already started are billed, including a call that's interrupted mid-generation.
- **Failed turns** : Single-call turns that end as `failed` , including turns that exceed the 24-hour completion window, aren't billed. In a multi-step server-side tool loop, completed model calls before a failure are billed, but the failed call isn't.
- **Chained turns** : Each turn in a `previous_interaction_id` chain is billed on its own. Cancelling a later turn, or a later turn failing, doesn't change the charges for earlier turns.

For per-model token rates, see the [Agent Platform pricing page](https://cloud.google.com/model-garden/pricing) .

### Quotas, payload limits, and retention

The Deferred tier doesn't have its own model-call quota. Deferred calls share the Flex pay-as-you-go quota ( `flex_requests_per_minute_per_project_per_base_model` , 3,000 RPM), which is checked on each model call after `interactions.create` returns `queued` . Key project quotas and system limits include the following:

- **Creation and concurrency quotas** : Up to 100 RPM or unlimited for `stateful_genai_interaction_creations` at creation time. Up to 500 `concurrent_interaction_generations` , depending on your quota tier.
- **Daily stateful throughput (fixed)** : 240 GiB per day written and 480 GiB per day read per project.
- **Payload and retention limits** : Up to 9.75 MiB uncompressed HTTP body per `interactions.create` call, and 7-day state retention. Chains support up to 100 distinct Cloud Storage ( `gs://` ) URIs.

For the complete quota table and console instructions, see [Deferred tier quotas and limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#deferred-tier-quotas) .

### Security and compliance controls

Because the Deferred tier queues and persists state on the `global` endpoint, verify that its supported governance controls match your compliance requirements:

- **Supported controls** : [VPC Service Controls](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/vpc-service-controls) (VPC-SC; external `mcp_server` tools aren't allowed inside a perimeter), [Access Transparency](https://docs.cloud.google.com/assured-workloads/access-transparency/docs/overview) (AXT), Cloud Audit Logs, and FedRAMP High.
- **Unsupported controls** : Stateless zero data retention ( `store=false` and enforcing `constraints/vertexai.disableAPIStorage` both return HTTP `400` with `"code": "invalid_request"` ), [Customer-managed encryption keys](https://docs.cloud.google.com/gemini-enterprise-agent-platform/machine-learning/general/cmek) (CMEK), [Data residency](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/data-residency) , DoD IL5, and ITAR.

For the full feature matrix, see [Security controls for Generative AI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/security-controls#deferred-tier) .

## Troubleshoot

The following table describes common errors on the Deferred tier and how to resolve them:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Error or status</th>
<th>Common causes</th>
<th>Resolution</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>400</code> ( <code>error.code: "invalid_request"</code> ; endpoint, flags, or model)</td>
<td>Non- <code>global</code> endpoint, unsupported model, or invalid <code>background</code> , <code>store</code> , or <code>stream</code> flags on <code>interactions.create</code> .</td>
<td>Target <code>locations/global</code> with a <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier#supported-models">supported model</a> , set <code>background=true</code> and <code>store=true</code> , and omit <code>stream=true</code> .</td>
</tr>
<tr class="even">
<td><code>400</code> ( <code>error.code: "invalid_request"</code> ; payload, URIs, or tools)</td>
<td>Uncompressed body exceeds 9.75 MiB, chain exceeds 100 <code>gs://</code> URIs, or external <code>mcp_server</code> tools inside VPC-SC.</td>
<td>Pass large files as <code>gs://</code> URIs (at most 100 per chain), and omit external <code>mcp_server</code> tools inside VPC-SC.</td>
</tr>
<tr class="odd">
<td><code>400</code> ( <code>error.code: "invalid_request"</code> on <code>interactions.create</code> ; <code>status: "FAILED_PRECONDITION"</code> on <code>interactions.delete</code> )</td>
<td><ul>
<li>The <code>constraints/vertexai.disableAPIStorage</code> policy is enforced.</li>
<li><code>interactions.create</code> chains onto a <code>queued</code> or <code>in_progress</code> turn, or sets <code>input</code> on <code>requires_continuation</code> .</li>
<li><code>interactions.delete</code> targets a <code>queued</code> or <code>in_progress</code> turn.</li>
</ul></td>
<td><ul>
<li>Use a project that allows API state persistence.</li>
<li>Chain only onto final turns. On <code>requires_continuation</code> , pass <code>continuation_token</code> and omit <code>input</code> .</li>
<li>Cancel active turns before you delete them.</li>
</ul></td>
</tr>
<tr class="even">
<td><code>401</code> ( <code>status: "UNAUTHENTICATED"</code> or <code>error.code: "authentication"</code> )</td>
<td>Your gcloud CLI credentials (REST samples) or ADC (Google Gen AI SDK samples) are missing or expired.</td>
<td>For REST samples, run <code>gcloud auth login</code> . For Google Gen AI SDK samples, run <code>gcloud auth application-default login</code> . Then retry the request.</td>
</tr>
<tr class="odd">
<td><code>403</code> ( <code>status: "PERMISSION_DENIED"</code> or <code>error.code: "permission_denied"</code> )</td>
<td><ul>
<li>The caller doesn't have <code>roles/aiplatform.user</code> .</li>
<li>The caller doesn't have <code>storage.objects.get</code> on <code>gs://</code> inputs.</li>
</ul></td>
<td>Grant <code>roles/aiplatform.user</code> . For Cloud Storage inputs, also grant <code>roles/storage.objectViewer</code> .</td>
</tr>
<tr class="even">
<td><code>404</code> ( <code>error.code: "not_found"</code> ; <code>status: "NOT_FOUND"</code> on <code>interactions.delete</code> )</td>
<td>The interaction or <code>previous_interaction_id</code> doesn't exist or was deleted. It might also belong to a non- <code>global</code> endpoint or be older than the 7-day retention period.</td>
<td>Check the interaction ID on the <code>global</code> endpoint. If the parent turn expired, start a new chain without <code>previous_interaction_id</code> .</td>
</tr>
<tr class="odd">
<td><code>409</code> ( <code>error.code: "aborted"</code> )</td>
<td><code>interactions.cancel</code> targets an interaction that's already in a final status: <code>requires_action</code> , <code>requires_continuation</code> , <code>completed</code> , <code>incomplete</code> , <code>failed</code> , or <code>cancelled</code> .</td>
<td>Check <code>status</code> with <code>interactions.get</code> first. You can cancel only <code>queued</code> and <code>in_progress</code> interactions.</td>
</tr>
<tr class="even">
<td><code>429</code> ( <code>error.code: "too_many_requests"</code> )</td>
<td>The project exceeded a per-project quota, such as the interaction creation rate, concurrent interaction generations, or daily stateful throughput.</td>
<td><ul>
<li>Retry after the <code>Retry-After</code> header delay with backoff and jitter.</li>
<li>Request adjustable quota increases in <a href="https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/quotas#deferred-tier-quotas">Deferred tier quotas and limits</a> . Daily throughput limits are fixed.</li>
</ul></td>
</tr>
<tr class="odd">
<td><code>status="failed"</code></td>
<td><ul>
<li>An upstream model or tool failure occurred, or the turn exceeded the 24-hour completion window.</li>
<li>The request uses a <code>*-cyber*</code> model, and the project doesn't have allowlist access.</li>
</ul></td>
<td><ul>
<li>Inspect the <code>error</code> field that <code>interactions.get</code> returns, and then submit a new <code>interactions.create</code> request.</li>
<li>For Cyber models, confirm allowlist access with your Google Cloud account team.</li>
</ul></td>
</tr>
</tbody>
</table>

## What's next

Explore related guides and reference documentation for asynchronous and stateful Gemini workloads:

- Compare compute models in [Consumption options](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deploy/consumption-options) .
- Build stateful multi-turn applications in the [Interactions API developer guide](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions/developer-guide) .
- Schedule ADK agents and managed research runs in [Autonomous agent scheduling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling) .
- Explore method schemas in the [Interactions API reference](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/models/interactions-api) .
