---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk
title: Use Memory Bank with ADK
description: Configure memory generation callbacks, retrieval tools, and runtimes so your ADK agent reads and writes Agent Platform Memory Bank memories.
data_source: docs.cloud.google.com
---

The Agent Development Kit (ADK) connects agents to Agent Platform Memory Bank through [`VertexAiMemoryBankService`](https://github.com/google/adk-python/blob/main/src/google/adk/memory/vertex_ai_memory_bank_service.py) , an implementation of the ADK [`BaseMemoryService`](https://github.com/google/adk-python/blob/main/src/google/adk/memory/base_memory_service.py) interface. This document explains how to choose a memory callback and retrieval tool, and how to connect the memory service in each ADK runtime.

To run a complete example first, see the [Memory Bank quickstart with ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart) .

## Before you begin

1.  If you're using a local shell, then create local authentication credentials for your user account:

    ```
    gcloud auth application-default login
    ```

    You don't need to do this if you're using Cloud Shell.

    > **Note:** If the gcloud CLI prints a warning that your account doesn't have the `serviceusage.services.use` permission, then some gcloud CLI commands and client libraries might not work. Ask an administrator to grant you the Service Usage Consumer IAM role ( `roles/serviceusage.serviceUsageConsumer` ), then run the following command:
    >
    > ```
    > gcloud auth application-default set-quota-project PROJECT_ID
    > ```

    If an authentication error is returned, and you are using an external identity provider (IdP), confirm that you have [signed in to the gcloud CLI with your federated identity](https://docs.cloud.google.com/iam/docs/workforce-log-in-gcloud) .

2.  Install ADK and the Agent Platform SDK:

    ```
    pip install --upgrade "google-adk[gcp]" "google-cloud-agentplatform>=2.0.1"
    ```

3.  [Create a Memory Bank instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#create-update) in the Google Cloud console or with the Agent Platform SDK. On the **Memory Bank** page, click **Link to an agent** \> **Use with ADK** for prefilled setup code. Skip this step if Agent Runtime creates the instance for you.

### Required roles

To get the permissions that you need to create a Memory Bank instance and generate and retrieve memories, ask your administrator to grant you the following IAM roles on your project:

- Create or update a Memory Bank instance: Agent Platform User (\`roles/aiplatform.user\`)
- Read, write, or generate memories: Memory Bank User (\`roles/aiplatform.memoryUser\`)

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## How ADK components work with Memory Bank

An ADK agent uses the following components to read and write memories:

| Component                   | Role                                                                                                                                                                                                                                   | Required          |
|-----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| Memory Bank instance        | Stores and consolidates memories.                                                                                                                                                                                                      | Yes               |
| `VertexAiMemoryBankService` | Connects your agent to Memory Bank as the ADK memory service.                                                                                                                                                                          | Yes               |
| Session service             | Stores conversation history. You can use any ADK session service.                                                                                                                                                                      | Yes               |
| Memory retrieval tool       | Retrieves memories for the agent. See [Retrieve memories with a tool](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk#memory-retrieval-tool) .                                           | To read memories  |
| Memory generation callback  | Sends conversation events to Memory Bank after the agent responds. See [Generate memories with a callback](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk#memory-generation-callback) . | To write memories |
| ADK Runner or `AdkApp`      | Orchestrates the agent, services, tools, and callbacks.                                                                                                                                                                                | Yes               |

The following diagram shows how these components interact on each turn when an agent uses `PreloadMemoryTool` and a memory callback:

Memory Bank scopes each memory to the user ID and app name that run your agent, as `{"user_id": USER_ID, "app_name": APP_NAME}` . Only requests with the same user ID and app name retrieve those memories.

## Generate memories with a callback

A memory generation callback sends conversation events to Memory Bank. Memory Bank extracts memories from those events and consolidates them with existing memories. Choose a method based on how often you process events:

| Method                                   | Events sent                        | When to use                                                                                 |
|------------------------------------------|------------------------------------|---------------------------------------------------------------------------------------------|
| `callback_context.add_events_to_memory`  | A subset of events that you select | Recommended. Process events incrementally, for example after each turn.                     |
| `callback_context.add_session_to_memory` | All events in the session          | Call once at the end of a session, so that the same events aren't processed more than once. |

The following example sends recent events after each agent response:

```
from google.adk.agents.callback_context import CallbackContext


async def generate_memories_callback(
    callback_context: CallbackContext,
) -> None:
    await callback_context.add_events_to_memory(
        events=callback_context.session.events[-5:]
    )
    return None
```

To send the full session instead, call `await callback_context.add_session_to_memory()` in a callback at the end of the session.

By default, `VertexAiMemoryBankService` sends events by using [event ingestion](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/ingest-events) . To wait until memory generation finishes in tests or demos, pass `custom_metadata={"wait_for_completion": True}` to `add_events_to_memory` .

## Retrieve memories with a tool

A memory retrieval tool controls when the agent retrieves memories and how the memories enter the prompt. Choose one of the following tools:

| Tool                  | When memories are retrieved                                                                                    | When to use                                                  |
|-----------------------|----------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------|
| `PreloadMemoryTool`   | At the start of every turn. Memories are injected into the model request context before the current user turn. | Establish baseline context about the user on every turn.     |
| `LoadMemoryTool`      | When the model decides that memories are necessary to answer the query.                                        | Let the model decide when memories are relevant.             |
| Custom `FunctionTool` | When the model calls your tool, guided by the tool's description.                                              | Give the agent instructions about when to retrieve memories. |

The following example creates an agent that uses `PreloadMemoryTool` and the callback from the preceding section:

```
from google import adk
from google.adk.tools.preload_memory_tool import PreloadMemoryTool

agent = adk.Agent(
    model="gemini-3.5-flash",
    name="stateful_agent",
    instruction="You are a vehicle voice agent. Limit responses to 30 words.",
    tools=[PreloadMemoryTool()],
    after_agent_callback=generate_memories_callback,
)
```

To let the model decide when to retrieve memories, import `LoadMemoryTool` from `google.adk.tools.load_memory_tool` and pass `LoadMemoryTool()` in `tools` .

To write a custom retrieval tool, call `tool_context.search_memory` from a function tool:

```
from typing import Any

from google import adk
from google.adk.tools import FunctionTool, ToolContext


async def search_memories(query: str, tool_context: ToolContext) -> Any:
    """Query this tool when you need information about user preferences."""
    return await tool_context.search_memory(query)


agent = adk.Agent(
    model="gemini-3.5-flash",
    name="stateful_agent",
    instruction=(
        "You are a vehicle voice agent. Before you change a setting, call "
        "search_memories to look up the user's preferences. Limit responses "
        "to 30 words."
    ),
    tools=[FunctionTool(func=search_memories)],
    after_agent_callback=generate_memories_callback,
)
```

## Connect the memory service to your runtime

How you connect `VertexAiMemoryBankService` depends on where your agent [runs](https://google.github.io/adk-docs/runtime/) . Select your runtime:

### Local runner

When you run your agent with `adk.Runner` , create the memory service and pass it to the runner:

```
import asyncio
import os

from google import adk
from google.adk.memory import VertexAiMemoryBankService
from google.adk.sessions import InMemorySessionService
from google.genai import types

os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
os.environ["GOOGLE_CLOUD_PROJECT"] = "PROJECT_ID"
os.environ["GOOGLE_CLOUD_LOCATION"] = "LOCATION"

memory_service = VertexAiMemoryBankService(
    project="PROJECT_ID",
    location="LOCATION",
    agent_engine_id="MEMORY_BANK_ID",
)

# You can use any ADK session service. This example keeps sessions in memory.
# To persist conversation history, use VertexAiSessionService with a
# Sessions instance instead.
session_service = InMemorySessionService()

runner = adk.Runner(
    agent=agent,
    app_name="APP_NAME",
    session_service=session_service,
    memory_service=memory_service,
)

async def main() -> None:
    session = await session_service.create_session(
        app_name="APP_NAME",
        user_id="USER_ID",
    )
    message = types.Content(
        role="user", parts=[types.Part(text="Can you fix the temperature?")]
    )
    async for event in runner.run_async(
        user_id="USER_ID",
        session_id=session.id,
        new_message=message,
    ):
        if event.is_final_response() and event.content:
            print(event.content.parts[0].text)

asyncio.run(main())
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID, for example `my-project` .
- ` LOCATION ` : Your location, for example `global` . See the [supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) and [global and multi-regional endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#multi-regional-global-endpoints) for Memory Bank.
- ` MEMORY_BANK_ID ` : The Memory Bank instance ID, for example `456` in `projects/my-project/locations/us-central1/reasoningEngines/456` .
- ` APP_NAME ` : The ADK app name, for example `my_agent` . Memory Bank includes the app name in the memory scope, so memories are isolated across apps.
- ` USER_ID ` : An identifier for your user, for example `user-123` . Memories generated from this session are scoped to this identifier.

### Agent Runtime on Gemini Enterprise Agent Platform

When you deploy an ADK agent to Agent Runtime with the [ADK template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent) ( `AdkApp` ), the template uses `VertexAiMemoryBankService` by default. You can create the Memory Bank instance and deploy the agent in one step:

```
import asyncio

import agentplatform
from agentplatform.frameworks import AdkApp

client = agentplatform.Client(
    project="PROJECT_ID",
    location="LOCATION",
)

adk_app = AdkApp(agent=agent)

# Create a resource with your agent deployed to Agent Runtime. The
# resource also includes an empty Memory Bank instance.
runtime_instance = client.runtimes.create(
    agent=adk_app,
    config={
        "staging_bucket": "STAGING_BUCKET",
        "requirements": ["google-cloud-agentplatform[runtimes,adk]"],
    },
)

async def main() -> None:
    session = await runtime_instance.async_create_session(
        user_id="USER_ID"
    )
    async for event in runtime_instance.async_stream_query(
        user_id="USER_ID",
        session_id=session.get("id"),
        message="Can you fix the temperature?",
    ):
        print(event)

asyncio.run(main())
```

To deploy the agent to an existing resource and keep the resource's existing memories, call `client.runtimes.update` instead:

```
runtime_instance = client.runtimes.update(
    name="RUNTIME_NAME",
    agent=adk_app,
    config={
        "staging_bucket": "STAGING_BUCKET",
        "requirements": ["google-cloud-agentplatform[runtimes,adk]"],
    },
)
```

When you run `AdkApp` locally, it uses `InMemoryMemoryService` by default. To use Memory Bank locally, override the memory service:

```
from google.adk.memory import VertexAiMemoryBankService

def memory_bank_service_builder() -> VertexAiMemoryBankService:
    return VertexAiMemoryBankService(
        project="PROJECT_ID",
        location="LOCATION",
        agent_engine_id="MEMORY_BANK_ID",
    )

adk_app = AdkApp(
    agent=agent,
    memory_service_builder=memory_bank_service_builder,
)
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID, for example `my-project` .
- ` LOCATION ` : Your Agent Runtime region or multi-region, for example `us-central1` . Only standalone `VertexAiMemoryBankService` instances support `global` , not `client.runtimes.create` . See [supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) .
- ` STAGING_BUCKET ` : The Cloud Storage bucket URI for staging your Agent Runtime, for example `gs://my-staging-bucket` .
- ` USER_ID ` : An identifier for your user, for example `user-123` .
- ` RUNTIME_NAME ` : The resource name of the existing Agent Runtime, in the format `projects/.../locations/.../reasoningEngines/...` .
- ` MEMORY_BANK_ID ` : The Memory Bank instance ID, for example `456` in `projects/my-project/locations/us-central1/reasoningEngines/456` .

### Cloud Run

> To see an example of using Memory Bank with Cloud Run, run the "Get started with Sessions and Memory Bank for ADK agents in Cloud Run" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/cloud_run/agents_with_memory/get_started_with_memory_for_adk_in_cloud_run.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fcloud_run%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_cloud_run.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fcloud_run%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_cloud_run.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/cloud_run/agents_with_memory/get_started_with_memory_for_adk_in_cloud_run.ipynb)

To deploy your agent to Cloud Run, follow the [ADK documentation](https://google.github.io/adk-docs/deploy/cloud-run/) and pass your Memory Bank instance as the memory service:

```
adk deploy cloud_run \
    ...
    --memory_service_uri=agentengine://MEMORY_BANK_ID
```

Replace ` MEMORY_BANK_ID ` with your Memory Bank instance ID, for example `456` . To test the deployed agent, see the [ADK Cloud Run deployment documentation](https://google.github.io/adk-docs/deploy/cloud-run/) .

### Google Kubernetes Engine (GKE)

> To see an example of using Memory Bank with Google Kubernetes Engine, run the "Get started with Sessions and Memory Bank for ADK agents in GKE" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/gke/agents_with_memory/get_started_with_memory_for_adk_in_gke.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fgke%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_gke.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fgke%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_gke.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/gke/agents_with_memory/get_started_with_memory_for_adk_in_gke.ipynb)

To deploy your agent to GKE, follow the [ADK documentation](https://google.github.io/adk-docs/deploy/gke/) and pass your Memory Bank instance as the memory service:

```
adk deploy gke \
    ...
    --memory_service_uri=agentengine://MEMORY_BANK_ID
```

Replace ` MEMORY_BANK_ID ` with your Memory Bank instance ID, for example `456` . To test the deployed agent, see the [Testing your agent](https://google.github.io/adk-docs/deploy/gke/#testing-your-agent) section of the ADK GKE deployment documentation.

### ADK Web

ADK Web is a local browser interface for testing and inspecting your agent during development.

> **Important:** ADK Web isn't meant for production deployments. Use ADK Web for development and debugging only.

ADK Web reads your project and location from environment variables. Run the following commands in your terminal, from the directory that contains your agent folder:

```
export GOOGLE_GENAI_USE_ENTERPRISE=TRUE
export GOOGLE_CLOUD_PROJECT=PROJECT_ID
export GOOGLE_CLOUD_LOCATION=LOCATION
adk web --memory_service_uri=agentengine://MEMORY_BANK_ID
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID, for example `my-project` .
- ` LOCATION ` : Your location, for example `global` . See the [supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) and [global and multi-regional endpoints](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#multi-regional-global-endpoints) for Memory Bank.
- ` MEMORY_BANK_ID ` : The Memory Bank instance ID, for example `456` .

Then open `http://localhost:8000` in your browser. By default, ADK Web sets the user ID to `user` . To use a different user ID, add the `userId` query parameter, for example `http://localhost:8000?userId=USER_ID` .

## Use a multi-regional Memory Bank with a regional runtime

By default, when you use Runtime with built-in Memory Bank, your agent and Memory Bank are deployed in the same region. To maintain one central Memory Bank across regional deployments, you can pair a multi-regional Memory Bank (such as `us` ) with a regional runtime (such as `us-central1` ).

To use a multi-regional Memory Bank, override the default ADK memory service builder so that it points to the multi-region location and instance ID:

```
import agentplatform
from agentplatform.frameworks import AdkApp
from google.adk.memory import VertexAiMemoryBankService

# Create the Memory Bank instance in a multi-region location.
client_mb = agentplatform.Client(
    project="PROJECT_ID",
    location="us",
)
memory_bank = client_mb.memory_banks.create()
memory_bank_id = memory_bank.name.split("/")[-1]


# Point the memory service to the multi-regional instance.
def memory_bank_service_builder() -> VertexAiMemoryBankService:
    return VertexAiMemoryBankService(
        project="PROJECT_ID",
        location="us",
        agent_engine_id=memory_bank_id,
    )


adk_app = AdkApp(
    agent=agent,
    memory_service_builder=memory_bank_service_builder,
)

# Deploy the runtime to a specific region.
client_runtime = agentplatform.Client(
    project="PROJECT_ID",
    location="us-central1",
)
runtime_instance = client_runtime.runtimes.create(
    agent=adk_app,
    config={
        "staging_bucket": "STAGING_BUCKET",
        "requirements": ["google-cloud-agentplatform[runtimes,adk]"],
    },
)
```

Replace the following:

- ` PROJECT_ID ` : Your Google Cloud project ID, for example `my-project` .
- ` STAGING_BUCKET ` : The Cloud Storage bucket URI for staging your Agent Runtime, for example `gs://my-staging-bucket` .

To delete these resources, delete the runtime and the multi-regional instance. If you delete an instance right after a conversation, the request can fail with a `FAILED_PRECONDITION` error while memory generation finishes. If that happens, wait a minute and run the deletion again.

```
client_runtime.runtimes.delete(
    name=runtime_instance.api_resource.name,
    force=True,
)
client_mb.memory_banks.delete(name=memory_bank.name, force=True)
```

## What's next

Quickstart

### [Quickstart with Agent Development Kit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart)

Build an ADK agent that recalls user preferences.

Guide

### [Generate memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories)

Learn how to generate memories in Memory Bank.

Guide

### [Set up Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup)

Learn how to set up Memory Bank.
