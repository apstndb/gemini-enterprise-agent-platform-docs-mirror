---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart
title: 'Quickstart: Add long-term memory to an ADK agent with Memory Bank'
description: Build an ADK agent that remembers a user preference across sessions with Agent Platform Memory Bank, and verify recall in a new session.
data_source: docs.cloud.google.com
---

Agent Platform Memory Bank gives agents that you build with the Agent Development Kit (ADK) long-term memory across sessions. In this quickstart, you run an agent that learns a user's preferred temperature in one session and recalls the preference in the next session.

This quickstart guides you through the following steps:

- Set up your environment.
- Create a Memory Bank instance.
- Run a memory-enabled ADK agent locally.
- Verify that the agent recalls the preference in a new session.

To call Memory Bank directly without ADK, see the [Memory Bank API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart) . To choose other memory tools, callbacks, or runtimes, see [Use Memory Bank with ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk) .

> To see an example of using Memory Bank with ADK, run the "Get started with Memory Bank on ADK" notebook in one of the following environments:
>
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank_on_adk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank_on_adk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank_on_adk.ipynb) \| [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank_on_adk.ipynb)

## Before you begin

1.  Set up a [Python development environment](https://docs.cloud.google.com/python/docs/setup) .

2.  If you're using a local shell, then create local authentication credentials for your user account:

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

> **Note:** To enable APIs, you need the `serviceusage.services.enable` permission. If you don't have this permission, ask your administrator to grant you the Service Usage Admin ( `roles/serviceusage.serviceUsageAdmin` ) role.

### Required roles

To get the permissions that you need to create a Memory Bank instance and generate and retrieve memories, ask your administrator to grant you the following IAM roles on your project:

- Create or update a Memory Bank instance: Agent Platform User (\`roles/aiplatform.user\`)
- Read, write, or generate memories: Memory Bank User (\`roles/aiplatform.memoryUser\`)

For more information about granting roles, see [Manage access to projects, folders, and organizations](https://docs.cloud.google.com/iam/docs/granting-changing-revoking-access) .

You might also be able to get the required permissions through [custom roles](https://docs.cloud.google.com/iam/docs/creating-custom-roles) or other [predefined roles](https://docs.cloud.google.com/iam/docs/roles-overview#predefined) .

## Set up your environment

1.  In your terminal, install ADK and the Agent Platform SDK:

    ```
    pip install --upgrade "google-adk[gcp]" "google-cloud-agentplatform>=2.0.1"
    ```

2.  Set the environment variables that the scripts in this quickstart read:

    ```
    export GOOGLE_GENAI_USE_ENTERPRISE=TRUE
    export GOOGLE_CLOUD_PROJECT=PROJECT_ID
    export GOOGLE_CLOUD_LOCATION=global
    ```

    Replace ` PROJECT_ID ` with your Google Cloud project ID.

    This quickstart uses the global endpoint. To use a regional or multi-regional location instead, replace `global` with one of the [supported locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) . If you need customer-managed encryption keys (CMEK), use a regional or multi-regional location, because CMEK isn't available with the global endpoint.

    Run the rest of this quickstart in the same terminal session and directory so that the scripts can read these variables.

## Create a Memory Bank instance

1.  Create a file named `create_memory_bank.py` with the following code:

    ```
    import os

    import agentplatform

    client = agentplatform.Client(
        project=os.environ["GOOGLE_CLOUD_PROJECT"],
        location=os.environ["GOOGLE_CLOUD_LOCATION"],
    )

    memory_bank = client.memory_banks.create(
        config={"display_name": "Memory Bank quickstart"}
    )

    # Print only the instance ID, for example 1234567890.
    print(memory_bank.name.split("/")[-1])
    ```

2.  Run the script and save the instance ID in the `MEMORY_BANK_ID` environment variable:

    ```
    export MEMORY_BANK_ID=$(python create_memory_bank.py)
    ```

    If this is your first Memory Bank instance, creation can take 1-2 minutes.

3.  Confirm that the variable contains the instance ID:

    ```
    echo $MEMORY_BANK_ID
    ```

    The output is an ID such as `1234567890` . If the output is empty or returns a `401` or `403` error, check your [required roles](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart#required-roles) and run `gcloud auth application-default login` . If a new `global` instance returns a transient `403` error on first use, wait 30 seconds and run the script again.

## Run a memory-enabled agent

The script in this section runs two sessions for the same user. In the first session, the user states a temperature preference. In the second session, the agent recalls that preference from Memory Bank.

Complete the following steps:

1.  Create a directory named `memory_agent` :

    ```
    mkdir memory_agent
    ```

2.  Create a file named `memory_agent/agent.py` with the following code. The code reads your project, location, and instance ID from the variables you set in [Set up your environment](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart#set-up-environment) and [Create a Memory Bank instance](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart#create-a-memory-bank-instance) . You don't need to edit the code.

    ```
    import asyncio
    import os

    import agentplatform
    from google import adk
    from google.adk.agents.callback_context import CallbackContext
    from google.adk.memory import VertexAiMemoryBankService
    from google.adk.sessions import InMemorySessionService
    from google.adk.tools.preload_memory_tool import PreloadMemoryTool
    from google.genai import types

    PROJECT_ID = os.environ["GOOGLE_CLOUD_PROJECT"]
    LOCATION = os.environ["GOOGLE_CLOUD_LOCATION"]
    MEMORY_BANK_ID = os.environ["MEMORY_BANK_ID"]
    # Memory Bank scopes memories to this app name and user ID.
    APP_NAME = "memory_agent"
    USER_ID = "quickstart_user"

    async def generate_memories_callback(
        callback_context: CallbackContext,
    ) -> None:
        # Send the latest turn to Memory Bank and wait until memory generation
        # finishes, so that the next session can retrieve the new memory.
        await callback_context.add_events_to_memory(
            events=callback_context.session.events[-5:],
            custom_metadata={"wait_for_completion": True},
        )
        return None

    root_agent = adk.Agent(
        model="gemini-3.5-flash",
        name="memory_agent",
        instruction=(
            "You are a vehicle voice agent that controls in-vehicle settings. "
            "Use what you know about the user's preferences. "
            "If you don't know the user's preferred temperature, ask for it. "
            "Limit responses to under 30 words."
        ),
        tools=[PreloadMemoryTool()],
        after_agent_callback=generate_memories_callback,
    )

    memory_service = VertexAiMemoryBankService(
        project=PROJECT_ID,
        location=LOCATION,
        agent_engine_id=MEMORY_BANK_ID,
    )
    session_service = InMemorySessionService()
    runner = adk.Runner(
        agent=root_agent,
        app_name=APP_NAME,
        session_service=session_service,
        memory_service=memory_service,
    )

    async def send_message(session_id: str, text: str) -> None:
        print(f"User: {text}")
        message = types.Content(role="user", parts=[types.Part(text=text)])
        async for event in runner.run_async(
            user_id=USER_ID, session_id=session_id, new_message=message
        ):
            if event.is_final_response() and event.content:
                print(f"Agent: {event.content.parts[0].text}")

    async def main() -> None:
        print("--- Session 1: share a preference ---")
        session = await session_service.create_session(
            app_name=APP_NAME, user_id=USER_ID
        )
        await send_message(session.id, "Can you fix the temperature?")
        await send_message(session.id, "I'm comfortable at 71 degrees.")

        print("--- Session 2: recall the preference ---")
        session = await session_service.create_session(
            app_name=APP_NAME, user_id=USER_ID
        )
        await send_message(session.id, "Fix the temperature.")

        print("--- Memories stored in Memory Bank ---")
        client = agentplatform.Client(project=PROJECT_ID, location=LOCATION)
        memory_bank_name = (
            f"projects/{PROJECT_ID}/locations/{LOCATION}"
            f"/reasoningEngines/{MEMORY_BANK_ID}"
        )
        results = client.memory_banks.memories.retrieve(
            name=memory_bank_name,
            scope={"app_name": APP_NAME, "user_id": USER_ID},
        )
        for retrieved_memory in results.page:
            print(f"* {retrieved_memory.memory.fact}")

    if __name__ == "__main__":
        asyncio.run(main())
    ```

    > **Note:** ADK primarily uses [asynchronous functions](https://google.github.io/adk-docs/runtime/#async-is-primary-run_async) . The script wraps its async calls in `asyncio.run()` , which creates and manages an event loop when you run a standard Python script. In a notebook such as Colaboratory, an event loop is already running, so replace `asyncio.run(main())` with `await main()` .

3.  Run the script:

    ```
    python memory_agent/agent.py
    ```

    The callback waits for memory generation to finish after each turn, so the memory is available when the second session starts.

## Verify that the agent remembers

When the script finishes, it prints both conversations and the stored memory to your terminal. Compare that output with the following examples to confirm that the agent recalled the preference in a new session.

In the first session, the agent doesn't have any memories for the user, so it asks for a temperature:

```
--- Session 1: share a preference ---
User: Can you fix the temperature?
Agent: Sure. What temperature would you like?
User: I'm comfortable at 71 degrees.
Agent: Okay, I've set the temperature to 71 degrees.
```

In the second session, the agent retrieves the memory from Memory Bank and sets the temperature to 71 degrees without asking. The stored memory appears at the end of the output:

```
--- Session 2: recall the preference ---
User: Fix the temperature.
Agent: Okay, I've set the temperature to 71 degrees, as you prefer.
--- Memories stored in Memory Bank ---
* I like the temperature to be 71 degrees.
```

The wording of agent responses and memories varies depending on the models that the agent and Memory Bank use.

## Optional: Chat with your agent in ADK Web

ADK Web is a browser-based interface for testing agents during development.

> **Important:** ADK Web isn't meant for production deployments. Use ADK Web for development and debugging only.

1.  In the same terminal session, from the directory that contains the `memory_agent` directory, run the following command:

    ```
    adk web --memory_service_uri=agentengine://$MEMORY_BANK_ID memory_agent
    ```

2.  In your browser, open `http://localhost:8000?userId=quickstart_user` .

    The `userId` query parameter matches the user ID in the script, so the agent can retrieve the memory that the script created.

3.  Send the message `Fix the temperature.` and confirm that the agent sets the temperature to 71 degrees without asking. The agent uses the preference that the script stored in [Run a memory-enabled agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart#run-agent) .

4.  To stop ADK Web, press <span class="kbd"> Control+C </span> in the terminal.

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used on this page, you can [delete the Google Cloud project](https://docs.cloud.google.com/resource-manager/docs/delete-restore-projects#shutting_down_projects) . Otherwise, delete the individual resources:

1.  Create a file named `clean_up.py` with the following code:

    ```
    import os

    import agentplatform

    project = os.environ["GOOGLE_CLOUD_PROJECT"]
    location = os.environ["GOOGLE_CLOUD_LOCATION"]
    memory_bank_id = os.environ["MEMORY_BANK_ID"]

    client = agentplatform.Client(project=project, location=location)
    client.memory_banks.delete(
        name=f"projects/{project}/locations/{location}/reasoningEngines/{memory_bank_id}",
        force=True,
    )
    ```

2.  Run the script to delete the Memory Bank instance:

    ```
    python clean_up.py
    ```

3.  Delete the local files that you created:

    ```
    rm -r memory_agent create_memory_bank.py clean_up.py
    ```

## What's next

Quickstart

### [Memory Bank API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart)

Get started with the Memory Bank API to manage long-term memories.

Guide

### [Use Memory Bank with ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/use-with-adk)

Choose callbacks, tools, and runtimes for ADK.

Guide

### [Generate memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories)

Learn how to generate memories in Memory Bank.

Guide

### [Set up Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup)

Learn how to set up Memory Bank.
