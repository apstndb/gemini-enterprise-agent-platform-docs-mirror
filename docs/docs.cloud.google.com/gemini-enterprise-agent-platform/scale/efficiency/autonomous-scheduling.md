---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling
title: Autonomous agent scheduling
description: Optimize your agentic workflows using the Gemini Enterprise Agent Platform deferred tier for off-peak scheduling.
data_source: docs.cloud.google.com
---

When deploying multi-step agentic workflows (such as large-scale document synthesis and long-running research), running background agents on real-time models can create unnecessary infrastructure pressure and trigger resource exhaustion (429) errors.

Gemini Enterprise Agent Platform offers a *deferred tier* , a throughput-optimized scheduler designed specifically for latency-tolerant workloads. Instead of treating long-running autonomous tasks with the same immediate urgency as a live chat query, the scheduler queues your complex multi-step agent workflows to off-peak hours to target high success rates and overall throughput.

When you submit a request using the deferred tier, the API accepts the task asynchronously and returns an interaction ID immediately. The deferred tier features the following:

- **Discounted rate** : You receive a 50% discount on model inference pricing compared to a standard request, so you can manage your agent cost in production. For more information, see [Pricing](https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing) .

- **Higher throughput** : The deferred tier mitigates 429s (model capacity constraints) and rate limits by moving your heavy, asynchronous workloads off-peak, freeing up Standard Tier quota for your real-time production needs.

- **Completion timeout** : The deferred tier targets completing 95% of tasks within 24 hours. If a task doesn't complete within this window, it expires and transitions to a `failed` state. The actual time spent in the queue depends on current regional cluster capacity and demand.

## Use cases

The deferred tier is a good fit for use cases that can tolerate hours of turnaround time, such as the following examples:

- **Finance** : Daily or weekly equity and market research.

- **Legal & compliance** : Multi-document regulatory and mergers and acquisitions due diligence.

- **Strategy** : Continuous competitive intelligence and trend synthesis.

- **Security** : Codebase vulnerability scanning and fix.

## Supported agents

You can configure autonomous agent scheduling for the following agents. Select an agent to jump to its setup instructions:

- [Agent Development Kit (ADK) agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#schedule-adk-agent)
- [Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#schedule-deep-research)

To run custom or third-party agent loops directly on Gemini models, see [Use the Deferred tier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier) .

## Schedule an ADK agent

In [ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/adk) , you set the `service_tier` parameter on `RunConfig` per invocation instead of configuring a fixed tier on the agent or model. Setting `service_tier=ServiceTier.DEFERRED` queues each model call in an off-peak capacity pool, whereas the default `ServiceTier.STANDARD` runs synchronously. This per-run setting lets one agent definition serve both interactive requests and offline batch workflows.

When you send a deferred request for an ADK agent, ADK automates background submission, polling, and retrieval for you:

1.  ADK submits the model request with background execution enabled, and the backend returns an interaction ID with `queued` or `in_progress` status.
2.  While the interaction remains pending, ADK polls the backend with exponential backoff.
3.  When the interaction reaches a final status, ADK converts the completed interaction into standard model response events that you consume through the runner interface.

This section covers the following tasks for scheduling ADK agents:

- [Review requirements and limitations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#adk-limitations) before enabling the deferred tier.
- [Run an ADK agent on the deferred tier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#run-adk-deferred) using `RunConfig(service_tier=ServiceTier.DEFERRED)` .
- [Deploy deferred ADK agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#deploy-adk-deferred) on Agent Runtime, Cloud Run, or Google Kubernetes Engine (GKE).
- [Enforce a client deadline](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/efficiency/autonomous-scheduling#adk-client-deadline) to bound client-side wait time.

For more information about `ServiceTier` configuration in ADK, see [Deferred scheduling](https://adk.dev/agents/models/google-gemini/deferred-schedule/) in the ADK documentation.

### Limitations for ADK agents

Consider the following requirements and limitations when scheduling ADK agents on the deferred tier:

- **Requires the Interactions API** : Serving tiers apply only to models configured for the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) , such as `Gemini(use_interactions_api=True)` . Standard content generation models and `ManagedAgent` ignore `service_tier` .
- **Incompatible with token streaming** : Deferred execution can't be combined with `StreamingMode.SSE` in `RunConfig` . When calling `/run_sse` , omit `streaming` or set `"streaming": false` . Passing `"streaming": true` with `"service_tier": "deferred"` returns HTTP `422 Unprocessable Entity` .
- **HTTP connection limits** : On `adk api_server` , `/run` and `/run_sse` hold the HTTP connection open during the queue wait. If a proxy or platform timeout closes the connection (such as Cloud Run's 60-minute limit), client polling stops. The backend interaction still runs to completion and incurs charges.
- **Per-turn queue latency** : In multi-turn or tool-calling workflows, each model turn submits a separate interaction request. Every turn incurs its own off-peak queue wait.
- **No in-flight resumption across restarts** : ADK doesn't persist in-flight interaction IDs in session storage or reattach to disconnected interactions. Stopping a client process abandons the pending poll loop, and a subsequent invocation starts a new interaction.

### Run an ADK agent on the deferred tier

To schedule an ADK agent on the deferred tier, configure your Gemini model with `use_interactions_api=True` and pass `RunConfig(service_tier=ServiceTier.DEFERRED)` when invoking the runner:

```
import asyncio

from google.adk.agents import LlmAgent
from google.adk.agents import RunConfig
from google.adk.apps import App
from google.adk.models import ServiceTier
from google.adk.models.google_llm import Gemini
from google.adk.runners import InMemoryRunner
from google.genai import types

root_agent = LlmAgent(
    name="batch_agent",
    model=Gemini(
        model="gemini-3.5-flash",
        use_interactions_api=True,
        client_kwargs={
            "enterprise": True,
            "project": "PROJECT_ID",
            "location": "global",
        },
    ),
    instruction="Process input documents and produce summaries.",
)

app = App(
    name="batch_app",
    root_agent=root_agent,
)

runner = InMemoryRunner(app=app)


async def main() -> None:
  session = await runner.session_service.create_session(
      app_name=app.name,
      user_id="user_123",
      session_id="session_456",
  )

  run_config = RunConfig(service_tier=ServiceTier.DEFERRED)

  async for event in runner.run_async(
      user_id="user_123",
      session_id=session.id,
      new_message=types.Content(
          role="user",
          parts=[
              types.Part.from_text(
                  text="Summarize quarterly performance metrics."
              )
          ],
      ),
      run_config=run_config,
  ):
    if event.content and event.content.parts:
      for part in event.content.parts:
        if part.text:
          print(part.text)


asyncio.run(main())
```

Replace `PROJECT_ID` with your Google Cloud project ID.

While the interaction status is `queued` or `in_progress` , `runner.run_async()` yields no events until the interaction completes. Verify that the deferred tier is active by checking for the following messages in your application logs:

- At `INFO` level, the interactions transport logs `Interaction `` INTERACTION_ID `` is queued; waiting for the result.` and `Interaction `` INTERACTION_ID `` reached status completed.` When debug logging is enabled, the request processor also logs `Using service_tier from run_config: ServiceTier.DEFERRED` .
- If `use_interactions_api=True` isn't set on the model, ADK ignores `service_tier` , proceeds with standard generation, and logs a warning that the model doesn't use the Interactions API.

### Deploy deferred ADK agents

You configure `service_tier` per request rather than on the agent definition, so one ADK agent package ( `use_interactions_api=True` ) can serve both real-time and deferred workloads. You can deploy this package to Agent Runtime, Cloud Run, or GKE.

The following table compares the deployment options for deferred ADK workloads:

| Deployment option                                                                                             | When to use                                                                                                                                                    | Execution model                                   | Maximum timeout                             | How to request the deferred tier                                                                   |
|---------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|---------------------------------------------|----------------------------------------------------------------------------------------------------|
| [Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) | Asynchronous background jobs where Agent Platform manages sessions, runs without keeping an HTTP connection open, and writes results directly to Cloud Storage | Managed background job ( `run_query_job` )        | 168 hours (7 days; 24 hours per model turn) | `"run_config": {"service_tier": "deferred"}` inside `input`                                        |
| [Cloud Run service](https://docs.cloud.google.com/run/docs/deploying)                                         | Serverless HTTPS endpoints that serve both interactive requests and deferred workloads completing within 60 minutes                                            | Serverless HTTP or SSE ( `adk deploy cloud_run` ) | 60 minutes (3,600 seconds)                  | `"service_tier": "deferred"` in the `/run` or `/run_sse` (with `"streaming": false` ) request body |
| [Cloud Run job](https://docs.cloud.google.com/run/docs/create-jobs)                                           | Serverless batch workloads without an HTTP connection that might wait longer than 60 minutes (up to 24 hours per model turn)                                   | Serverless batch container ( `gcloud run jobs` )  | 168 hours (7 days)                          | `RunConfig(service_tier=ServiceTier.DEFERRED)`                                                     |
| [GKE](https://docs.cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview)               | Kubernetes workloads requiring custom networking, pod lifecycle control, or no serverless request timeout limits                                               | Kubernetes pods ( `adk deploy gke` )              | Unlimited (pod and ingress configured)      | `"service_tier": "deferred"` in the `/run` or `/run_sse` (with `"streaming": false` ) request body |

If your model uses the `global` endpoint while your deployment runs in a regional endpoint (such as `us-central1` ), pass `client_kwargs={"location": "global"}` to `Gemini(...)` . Make sure your runtime service account has the Agent Platform User ( `roles/aiplatform.user` ) role on your project.

Select a deployment target to view configuration instructions:

### Agent Runtime

When deploying your agent to [Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) , set `agent_framework="google-adk"` and include `google-adk>=2.10.0` in `requirements` . Grant the Reasoning Engine service agent ( `service- `` PROJECT_NUMBER `` @gcp-sa-aiplatform-re.iam.gserviceaccount.com` ) the Storage Object Creator ( `roles/storage.objectCreator` ) role on the output bucket.

To submit an asynchronous deferred [long-running query job](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-adk-agent#start-long-running-query-job) , call `client.runtimes.run_query_job()` and pass `"run_config": {"service_tier": "deferred"}` inside `input` :

```
import json
import agentplatform

client = agentplatform.Client(
    project="PROJECT_ID",
    location="LOCATION",
)

job = client.runtimes.run_query_job(
    name=(
        "projects/PROJECT_ID"
        "/locations/LOCATION"
        "/reasoningEngines/RESOURCE_ID"
    ),
    config={
        "query": json.dumps({
            "class_method": "async_stream_query",
            "input": {
                "user_id": "USER_ID",
                "session_id": "SESSION_ID",
                "message": "Summarize quarterly performance metrics.",
                "run_config": {"service_tier": "deferred"},
            },
        }),
        "output_gcs_uri": (
            "gs://BUCKET_NAME"
            "/OUTPUT_FILE.jsonl"
        ),
    },
)
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `LOCATION` : the supported region where your agent is deployed, such as `us-central1` .
- `RESOURCE_ID` : the numeric ID of your deployed `reasoningEngine` resource.
- `USER_ID` and `SESSION_ID` : the user and session identifiers for the invocation.
- `BUCKET_NAME` and `OUTPUT_FILE` : the Cloud Storage bucket and object prefix where Agent Runtime writes streamed events as newline-delimited JSON ( `application/x-ndjson` , one JSON object per line).

> **Caution:** On Agent Runtime, place `service_tier` inside `input.run_config` ( `"run_config": {"service_tier": "deferred"}` ). Placing `service_tier` at the top level of the job payload is ignored and runs on the `standard` tier.

### Cloud Run

Configure either a Cloud Run service or a Cloud Run job based on expected queue duration:

- **Cloud Run service ( `adk deploy cloud_run` )** : Deploys `adk api_server` behind an HTTPS endpoint ( `/run` and `/run_sse` ). Pass `-- --timeout=3600` when deploying so Cloud Run doesn't close the HTTP connection after the default 5-minute timeout:

  ```
  adk deploy cloud_run \
    --project=PROJECT_ID \
    --region=LOCATION \
    --service_name=SERVICE_NAME \
    AGENT_DIR \
    -- --no-allow-unauthenticated --timeout=3600
  ```

  Replace the following:

  - `PROJECT_ID` : your Google Cloud project ID.
  - `LOCATION` : the Cloud Run region, such as `us-central1` .
  - `SERVICE_NAME` : your Cloud Run service name.
  - `AGENT_DIR` : the path to your agent source directory.

  Before calling `/run` or `/run_sse` , create a session with `POST /apps/ `` APP_NAME `` /users/ `` USER_ID `` /sessions` , where `APP_NAME` defaults to your agent directory name. To request deferred execution, include `"service_tier": "deferred"` as a top-level field in the JSON request body. When calling `/run_sse` , omit `streaming` or set `"streaming": false` (passing `"streaming": true` returns HTTP `422 Unprocessable Entity` ):

  ```
  {
    "app_name": "batch_app",
    "user_id": "user_123",
    "session_id": "session_456",
    "new_message": {
      "role": "user",
      "parts": [{"text": "Summarize batch results."}]
    },
    "service_tier": "deferred",
    "streaming": false
  }
  ```

- **Cloud Run job ( `gcloud run jobs deploy` )** : Runs a container to completion without an HTTP request lifecycle and supports `--task-timeout` up to 168 hours (7 days). Pass `RunConfig(service_tier=ServiceTier.DEFERRED)` to `runner.run_async()` in your job entrypoint and deploy with `--task-timeout=86400s` (24 hours).

### GKE

Package and deploy your ADK agent to a GKE cluster using `adk deploy gke` :

```
adk deploy gke \
  --project=PROJECT_ID \
  --region=LOCATION \
  --cluster_name=CLUSTER_NAME \
  --service_name=SERVICE_NAME \
  AGENT_DIR
```

Replace the following:

- `PROJECT_ID` : your Google Cloud project ID.
- `LOCATION` : the region of your regional GKE cluster, such as `us-central1` .
- `CLUSTER_NAME` : the name of your GKE cluster.
- `SERVICE_NAME` : the Kubernetes service name for your agent.
- `AGENT_DIR` : the path to your agent source directory.

Before calling `/run` or `/run_sse` , create a session with `POST /apps/ `` APP_NAME `` /users/ `` USER_ID `` /sessions` , where `APP_NAME` defaults to your agent directory name. To request deferred execution, include `"service_tier": "deferred"` as a top-level field in the JSON request body. When calling `/run_sse` , omit `streaming` or set `"streaming": false` (passing `"streaming": true` returns HTTP `422 Unprocessable Entity` ):

```
{
  "app_name": "batch_app",
  "user_id": "user_123",
  "session_id": "session_456",
  "new_message": {
    "role": "user",
    "parts": [{"text": "Summarize batch results."}]
  },
  "service_tier": "deferred",
  "streaming": false
}
```

Requests to `/run` and `/run_sse` hold the HTTP connection open during the queue wait and model execution. Increase your GKE ingress and load balancer backend timeouts to accommodate expected queue delays. If the client connection closes or times out, the server cancels local polling. The backend interaction still runs and incurs charges without returning an output.

### Enforce a client deadline

ADK doesn't apply a client-side timeout to the queue wait, relying instead on the backend's 24-hour completion timeout. To bound total elapsed wait time in your application, wrap `runner.run_async()` in `asyncio.timeout()` :

```
import asyncio
import logging

from google.adk.agents import RunConfig
from google.adk.models import ServiceTier
from google.genai import types

logger = logging.getLogger(__name__)


# Continues from the earlier example using existing runner and session objects:
async def run_with_deadline(runner, session) -> None:
  message = types.Content(
      role="user",
      parts=[
          types.Part.from_text(text="Generate quarterly financial summary.")
      ],
  )
  run_config = RunConfig(service_tier=ServiceTier.DEFERRED)

  try:
    async with asyncio.timeout(300):
      async for event in runner.run_async(
          user_id="user_123",
          session_id=session.id,
          new_message=message,
          run_config=run_config,
      ):
        if event.content and event.content.parts:
          for part in event.content.parts:
            if part.text:
              print(part.text)
  except TimeoutError:
    logger.error(
        "Client timeout exceeded after 300 seconds. The deferred interaction"
        " continues to run and incur billing on the backend, so its output"
        " cannot be retrieved."
    )
```

Enforcing a client timeout stops the client-side polling loop at the next sleep interval, but doesn't cancel work on the backend. Even after a client timeout, the interaction continues running to completion and incurring charges on the server.

## Schedule the Gemini Deep Research Agent

Use the [Interactions API](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) to create, monitor, cancel, and retrieve results from a deferred Deep Research task.

### Create a deferred task

The following example shows how to [start a Deep Research task](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research#start-research-task) using the deferred tier with `client.interactions.create()` :

```
import time
from google import genai

client = genai.Client(
    enterprise=True,
    project="PROJECT_ID",
    location="global",
)

PROMPT = "Analyze the latest market trends in renewable energy storage."
DEEP_RESEARCH_AGENT = "deep-research-preview-04-2026"

interaction = client.interactions.create(
    input=PROMPT,
    agent=DEEP_RESEARCH_AGENT,  # Agent identifier
    service_tier="deferred",  # Run on deferred tier for off-peak scheduling
    background=True,  # Return immediately instead of waiting for the answer
    store=True,  # Persist interaction state to poll or stream later
    stream=False,  # `stream` must be set to False during task creation
)

print(f"Interaction ID: {interaction.id}")
print(f"Status:         {interaction.status}")
print(f"Service tier:   {interaction.service_tier}")
```

Replace `PROJECT_ID` with your Google Cloud project ID.

The method returns immediately with `status="queued"` or `status="in_progress"` and `service_tier="deferred"` .

### Monitor task progress

While awaiting off-peak capacity and actively running, the interaction `status` is `queued` or `in_progress` . As the agent executes planning, search, and analysis steps, new items append to the `steps` list.

You can track the task status programmatically by polling the interaction periodically or streaming updates.

### Polling

Poll the interaction periodically (such as every 15–30 seconds) until the interaction reaches one of the terminal states: `completed` , `failed` , `cancelled` , or `incomplete` .

```
TERMINAL_STATES = ("completed", "failed", "cancelled", "incomplete")
POLL_INTERVAL_SECONDS = 15
TIMEOUT_MINUTES = 60

started = time.time()
deadline = started + TIMEOUT_MINUTES * 60

while True:
  current = client.interactions.get(interaction.id)
  elapsed = int(time.time() - started)
  steps = getattr(current, "steps", None) or []
  print(f"[{elapsed:>4}s] status={current.status} steps={len(steps)}")

  if current.status in TERMINAL_STATES:
    break
  if time.time() >= deadline:
    raise TimeoutError(
        f"Still {current.status} after {TIMEOUT_MINUTES} min. The interaction "
        "continues running server-side; re-run the check to resume polling."
    )
  time.sleep(POLL_INTERVAL_SECONDS)

print(f"\nFinished in {int(time.time() - started)}s with status={current.status}.")
```

### Streaming

You can subscribe to real-time updates by calling `client.interactions.get()` with `stream=True` . Once the interaction enters `in_progress` status, the stream pushes events such as intermediate thoughts, text deltas, and status updates as they occur.

If the connection drops while the task is still `queued` or `in_progress` , reconnect to the stream using `client.interactions.get()` with `stream=True` and pass the last received event ID to `last_event_id` . If you omit `last_event_id` , the API replays every event from the beginning.

```
INTERACTION_ID = interaction.id  # from the create step
MAX_RECONNECTS = 5
STREAM_TIMEOUT = 300  # seconds

print(
    f"streaming interaction: {INTERACTION_ID} (status={interaction.status})\n"
)

def render(event):
  """Prints one SSE event. Returns True once the interaction has finished."""
  if event.event_type == "step.delta":
    delta = event.delta
    if delta.type == "text":
      print(delta.text, end="", flush=True)
    elif delta.type == "thought_summary":
      summary = (getattr(delta.content, "text", "") or "").strip()
      if summary:
        print(f"\n[thinking] {summary[:200]}", flush=True)
    elif delta.type.endswith("_call"):
      queries = getattr(getattr(delta, "arguments", None), "queries", None)
      print(
          f"\n[{delta.type}] {', '.join(queries) if queries else ''}",
          flush=True,
      )
  elif event.event_type == "interaction.status_update":
    print(f"[status] {event.status}", flush=True)
  elif event.event_type == "interaction.completed":
    print(f"\n\n[status] {event.interaction.status}", flush=True)
    return True
  elif event.event_type == "error":
    print(f"\n[error] {event.error.message}", flush=True)
    return True
  return False

last_event_id = None
finished = False

for attempt in range(MAX_RECONNECTS):
  try:
    # stream=True turns the GET into a live subscription. last_event_id=None on
    # the first pass, so the server starts from the beginning of the run.
    for event in client.interactions.get(
        INTERACTION_ID,
        stream=True,
        last_event_id=last_event_id,
        timeout=STREAM_TIMEOUT,
    ):
      last_event_id = event.event_id or last_event_id
      finished = render(event) or finished
  except Exception as e:  # pylint: disable=broad-except
    # A dropped connection loses nothing: the run continues server-side and the
    # next iteration reattaches from last_event_id.
    print(f"\n[stream dropped: {type(e).__name__}] reattaching...", flush=True)

  if finished:
    break
  # The server also closes the stream when the run ends, without an error.
  if client.interactions.get(
      INTERACTION_ID, timeout=STREAM_TIMEOUT
  ).status not in ("queued", "in_progress"):
    break
else:
  print(f"\n[gave up after {MAX_RECONNECTS} reconnects]")

print(f"\n\nStreamed interaction: {INTERACTION_ID}")
```

### Cancel a task

You can cancel a task while its status is `queued` , `in_progress` , or `requires_action` . When you cancel a task, its status transitions to `cancelled` .

To cancel a task, use `client.interactions.cancel()` :

```
client.interactions.cancel(interaction.id)
```

### Retrieve the final output and token usage

When the interaction reaches the `completed` state, the full transcript is available in the `steps` list. The final answer is the text content of the last `model_output` step.

Because the interaction is stored ( `store=True` ), you can fetch the result at any time using the interaction ID from any session:

```
def get_final_text(completed_interaction):
  """Returns the text of the last model_output step."""
  for step in reversed(getattr(completed_interaction, "steps", None) or []):
    if getattr(step, "type", None) != "model_output":
      continue
    text = "".join(
        part.text
        for part in (getattr(step, "content", None) or [])
        if getattr(part, "text", None)
    )
    if text:
      return text
  return ""


final = client.interactions.get(interaction.id)
print(f"Status: {final.status}\n")
print(get_final_text(final) or "(No text output)")

if final.usage:
  print(
      f"\nToken usage:\n"
      f"  Input tokens:  {final.usage.total_input_tokens}\n"
      f"  Output tokens: {final.usage.total_output_tokens}\n"
      f"  Total tokens:  {final.usage.total_tokens}"
  )
```

## What's next

Explore related guides for asynchronous model calls, stateful interactions, and managed research agents:

- Run asynchronous model calls for custom and third-party agents in [Use the Deferred tier](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/deferred-tier) .
- Review core session, tool, and state concepts in the [Interactions API overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/capabilities/interactions) .
- Plan and synthesize multi-step research workflows in [Use the Gemini Deep Research Agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/use-deep-research) .
