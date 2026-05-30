---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart
title: Agent Platform Memory Bank quickstart with Agent Development Kit
description: Learn how to create an agent using the Agent Development Kit (ADK) and integrate it with Agent Platform Memory Bank to manage long-term memories.
data_source: docs.cloud.google.com
---

Agent Platform Memory Bank allows your agents to manage long-term memories across sessions. When used with the Agent Development Kit (ADK), your agent can automatically orchestrate calls to Memory Bank to store and retrieve memories based on user interactions.

This document explains how to create an ADK agent, configure it to use Memory Bank, and interact with it to generate and access memories.

For information on making direct calls to the API without ADK, see the [Memory Bank API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart) .

> **Important:** ADK primarily uses [asynchronous functions](https://google.github.io/adk-docs/runtime/#async-is-primary-run_async) . If you're running code in a notebook like Colab, you can directly `await` async functions because an event loop is already running. If you're running this code as a standard Python script, you need to wrap your async function calls with `asyncio.run()` to create and manage an event loop to execute your async functions. Otherwise, you might get an error like `'await' outside function` .

> To see an example of using Memory Bank with ADK, run the "Get started with Memory Bank on ADK" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank_on_adk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank_on_adk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank_on_adk.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank_on_adk.ipynb)

## Manage memories with ADK memory service and Memory Bank

[`VertexAiMemoryBankService`](https://github.com/google/adk-python/blob/main/src/google/adk/memory/vertex_ai_memory_bank_service.py) is an ADK wrapper around Memory Bank that is defined by ADK's [`BaseMemoryService`](https://github.com/google/adk-python/blob/main/src/google/adk/memory/base_memory_service.py) . You can define callbacks and tools that interact with the memory service to read and write memories.

The `VertexAiMemoryBankService` interface includes:

  - `memory_service.add_session_to_memory` triggers a [`GenerateMemories`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) request to Memory Bank using all of the events in the provided `adk.Session` as the source content. You can orchestrate calls to this method using `callback_context.add_session_to_memory` in your callbacks.
    
        from google.adk.agents.callback_context import CallbackContext
        
        async def add_session_to_memory_callback(callback_context: CallbackContext):
            await callback_context.add_session_to_memory()
            return None

  - `memory_service.add_events_to_memory` which triggers a [`GenerateMemories`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) request to Memory Bank using a subset of events. You can orchestrate calls to this method using `callback_context.add_events_to_memory` in your callbacks.
    
        from google.adk.agents.callback_context import CallbackContext
        
        async def add_events_to_memory_callback(callback_context: CallbackContext):
            await callback_context.add_events_to_memory(events=callback_context.session.events[-5:-1])
            return None

  - `memory_service.search_memory` triggers a [`RetrieveMemories`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#scope-based) request to Memory Bank to fetch relevant memories for the current `user_id` and `app_name` . You can orchestrate calls to this method using built-in memory tools ( `LoadMemoryTool` or `PreloadMemoryTool` ) or a custom tool that invokes `tool_context.search_memory` .

## Before you begin

To complete the steps demonstrated in this tutorial, you must first follow the steps in the [getting started section of the Set up Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#get-started) page.

### Set environment variables

To use ADK, set your environment variables:

    import os
    
    os.environ["GOOGLE_GENAI_USE_ENTERPRISE"] = "TRUE"
    os.environ["GOOGLE_CLOUD_PROJECT"] = "PROJECT_ID"
    os.environ["GOOGLE_CLOUD_LOCATION"] = "LOCATION"

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.

## Create your ADK agent

To create a memory-enabled agent, set up tools and callbacks that orchestrate calls to your memory service.

### Define a memory generation callback

To orchestrate calls for memory generation, create a callback function that triggers memory generation. You can either send a subset of events (with `callback_context.add_events_to_memory` ) or all of the events in a session (with `callback_context.add_session_to_memory` ) to be processed in the background:

    from google.adk.agents.callback_context import CallbackContext
    
    async def generate_memories_callback(callback_context: CallbackContext):
        # Option 1 (Recommended): Send events to Memory Bank for memory generation,
        # which is ideal for incremental processing of events.
        await callback_context.add_events_to_memory(
          events=callback_context.session.events[-5:-1])
    
        # Option 2: Send the full session to Memory Bank for memory generation.
        # It's recommended to only call this at the end of a session to minimize
        # how many times a single event is re-processed.
        await callback_context.add_session_to_memory()
    
        return None

### Define a memory retrieval tool

When [developing your ADK agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent) , include a memory tool that controls when the agent retrieves memories and how memories are included in the prompt.

If you use `PreloadMemoryTool` , your agent will retrieve memories at the start of each turn and include the retrieved memories in the system instruction, which is good for establishing baseline context about the user. If you use `LoadMemoryTool` , the model will call this tool when it decides that memories are necessary to answer the user query.

    from google import adk
    from google.adk.tools.load_memory_tool import LoadMemoryTool
    from google.adk.tools.preload_memory_tool import PreloadMemoryTool
    
    memory_retrieval_tools = [
      # Option 1: Retrieve memories at the start of every turn.
      PreloadMemoryTool(),
      # Option 2: Retrieve memories via tool calls. The model will only call this tool
      # when it decides that memories are necessary to respond to the user query.
      LoadMemoryTool()
    ]
    
    agent = adk.Agent(
        model="gemini-2.5-flash",
        name='stateful_agent',
        instruction="""You are a Vehicle Voice Agent, designed to assist users with information and in-vehicle actions.
    
    1.  **Direct Action:** If a user requests a specific vehicle function (e.g., "turn on the AC"), execute it immediately using the corresponding tool. You don't have the outcome of the actual tool execution, so provide a hypothetical tool execution outcome.
    2.  **Information Retrieval:** Respond concisely to general information requests with your own knowledge (e.g., restaurant recommendation).
    3.  **Clarity:** When necessary, try to seek clarification to better understand the user's needs and preference before taking an action.
    4.  **Brevity:** Limit responses to under 30 words.
    """,
        tools=memory_retrieval_tools,
        after_agent_callback=generate_memories_callback
    )

Alternatively, you can create your own custom tool to retrieve memories, which is helpful for when you want to provide instructions to your agent on when to retrieve memories:

    from google import adk
    from google.adk.tools import ToolContext, FunctionTool
    
    async def search_memories(query: str, tool_context: ToolContext):
      """Query this tool when you need to fetch information about user preferences."""
      return await tool_context.search_memory(query)
    
    agent = adk.Agent(
        model="gemini-2.5-flash",
        name='stateful_agent',
        instruction="""...""",
        tools=[FunctionTool(func=search_memories)],
        after_agent_callback=generate_memories_callback
    )

## Define an ADK Memory Bank memory service and runtime

After you've created your memory-enabled agent, you need to link it to a memory service. The process of configuring your ADK memory service depends on where your ADK agent [runs](https://google.github.io/adk-docs/runtime/) , which orchestrates the execution of your agents, tools, and callbacks.

### Create an Agent Runtime instance

> **Note:** Skip this section if you already have an existing Agent Runtime instance that you want to use for Memory Bank.

You first need to create an Agent Runtime instance to use for Memory Bank. This step is optional if you're using Agent Runtime Runtime to deploy your agent. For more information on customizing your Memory Bank behavior, see the [Configure your Agent Runtime instance for Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#memory-bank-config) section on the Set up Memory Bank page.

    import vertexai
    
    client = vertexai.Client(
      project="PROJECT_ID",
      location="LOCATION"
    )
    # If you don't have an Agent Runtime instance already, create an Agent Platform
    # Memory Bank instance using the default configuration.
    agent_engine = client.agent_engines.create()
    
    # Optionally, print out the resource name. You will need the
    # resource name if you want to interact with your Runtime instance later on.
    print(agent_engine.api_resource.name)
    
    agent_engine_id = agent_engine.api_resource.name.split("/")[-1]

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.

### Create an ADK runtime

Pass the Agent Runtime ID to the runtime or deployment scripts so that your agent uses Memory Bank as the ADK memory service.

### Local runner

`adk.Runner` is generally used in a local environment, like Colab. In this case, you need to directly create the memory service and runner.

    import asyncio
    
    from google.adk.memory import VertexAiMemoryBankService
    from google.adk.sessions import VertexAiSessionService
    from google.genai import types
    
    memory_service = VertexAiMemoryBankService(
        project="PROJECT_ID",
        location="LOCATION",
        agent_engine_id="AGENT_ENGINE_ID",
    )
    
    # You can use any ADK session service. This example uses Sessions.
    session_service = VertexAiSessionService(
        project="PROJECT_ID",
        location="LOCATION",
        agent_engine_id="AGENT_ENGINE_ID",
    )
    
    runner = adk.Runner(
        agent=agent,
        app_name="APP_NAME",
        session_service=session_service,
        memory_service=memory_service
    )
    
    async def call_agent(query, session, user_id):
      content = types.Content(role='user', parts=[types.Part(text=query)])
      events = runner.run_async(
        user_id=user_id, session_id=session, new_message=content)
    
      async for event in events:
          if event.is_final_response():
              final_response = event.content.parts[0].text
              print("Agent Response: ", final_response)

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.
  - APP\_NAME : ADK app name. The app name will be included in the generated memories' `scope` dictionary so that memories are isolated across both users and apps.
  - AGENT\_ENGINE\_ID : The Agent Runtime ID to use for Memory Bank and Agent Platform Sessions. For example, `456` in `projects/my-project/locations/us-central1/reasoningEngines/456` .

### Agent Runtime

The [Agent Runtime ADK template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent) ( `AdkApp` ) can be used both locally and to deploy an ADK agent to Agent Runtime. When deployed on Agent Platform, the [Agent Runtime ADK template](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent) uses `VertexAiMemoryBankService` as the default memory service, using the same Runtime instance for Memory Bank as the runtime. So, you can create your Memory Bank instance and deploy to a runtime in a single step.

See [Configure Agent Runtime](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#configure-agent-engine) for more details on setting up your Agent Runtime instance, including how to customize the behavior of your Memory Bank.

Use the following code to deploy your memory-enabled ADK agent to Agent Runtime:

    import asyncio
    
    import vertexai
    from vertexai.agent_engines import AdkApp
    
    client = vertexai.Client(
      project="PROJECT_ID",
      location="LOCATION"
    )
    
    adk_app = AdkApp(agent=agent)
    
    # Create a new resource with your agent deployed to Agent Runtime.
    # The Agent Runtime instance will also include an empty Memory Bank.
    agent_engine = client.agent_engines.create(
          agent_engine=adk_app,
          config={
                "staging_bucket": "STAGING_BUCKET",
                "requirements": ["google-cloud-aiplatform[agent_engines,adk]"]
          }
    )
    
    # Alternatively, update an existing resource to deploy your agent to Agent Platform.
    # Your agent will have access to the Runtime instance's existing memories.
    agent_engine = client.agent_engines.update(
          name=agent_engine.api_resource.name,
          agent_engine=adk_app,
          config={
                "staging_bucket": "STAGING_BUCKET",
                "requirements": ["google-cloud-aiplatform[agent_engines,adk]"]
          }
    )
    
    async def call_agent(query, session_id, user_id):
        async for event in agent_engine.async_stream_query(
            user_id=user_id,
            session_id=session_id,
            message=query,
        ):
            print(event)

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.
  - STAGING\_BUCKET : Your Cloud Storage bucket to use for staging your Agent Runtime.

When run locally, the ADK template uses `InMemoryMemoryService` as the default memory service. However, you can override the default memory service to use `VertexAiMemoryBankService` :

    def memory_bank_service_builder():
        return VertexAiMemoryBankService(
            project="PROJECT_ID",
            location="LOCATION",
            agent_engine_id="AGENT_ENGINE_ID"
        )
    
    adk_app = AdkApp(
          agent=adk_agent,
          # Override the default memory service.
          memory_service_builder=memory_bank_service_builder
    )
    
    async def call_agent(query, session_id, user_id):
      # adk_app is a local agent. If you want to deploy it to Agent Runtime,
      # use `client.agent_engines.create(...)` or `client.agent_engines.update(...)`
      # and call the returned Agent Runtime instance instead.
      async for event in adk_app.async_stream_query(
          user_id=user_id,
          session_id=session_id,
          message=query,
      ):
          print(event)

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.
  - AGENT\_ENGINE\_ID : The Agent Runtime ID to use for Memory Bank. For example, `456` in `projects/my-project/locations/us-central1/reasoningEngines/456` .

### Cloud Run

> To see an example of using Memory Bank with Cloud Run, run the "Get started with Sessions and Memory Bank for ADK agents in Cloud Run" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/cloud_run/agents_with_memory/get_started_with_memory_for_adk_in_cloud_run.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fcloud_run%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_cloud_run.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fcloud_run%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_cloud_run.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/cloud_run/agents_with_memory/get_started_with_memory_for_adk_in_cloud_run.ipynb)

To deploy your agent to Cloud Run, refer to the instructions in the [ADK documentation](https://google.github.io/adk-docs/deploy/cloud-run/) to learn how to define your agent to deploy to Cloud Run.

    adk deploy cloud_run \
        ...
        --memory_service_uri=agentengine://AGENT_ENGINE_ID

### GKE

> To see an example of using Memory Bank with Google Kubernetes Engine, run the "Get started with Sessions and Memory Bank for ADK agents in Google Kubernetes Engine" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/gke/agents_with_memory/get_started_with_memory_for_adk_in_gke.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fgke%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_gke.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fgke%2Fagents_with_memory%2Fget_started_with_memory_for_adk_in_gke.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/gke/agents_with_memory/get_started_with_memory_for_adk_in_gke.ipynb)

To deploy your agent to Google Kubernetes Engine (GKE), refer to the instructions in the [ADK documentation](https://google.github.io/adk-docs/deploy/gke/) to learn how to define your agent to deploy to GKE.

    adk deploy gke \
        ...
        --memory_service_uri=agentengine://AGENT_ENGINE_ID

### ADK Web

> **Important:** ADK Web is not meant for use in production deployments. You should use ADK Web for development and debugging purposes only.

The [ADK web interface](https://google.github.io/adk-docs/runtime/web-interface/) lets you test your agents directly in the browser.

    export GOOGLE_CLOUD_PROJECT="PROJECT_ID"
    export GOOGLE_CLOUD_LOCATION="LOCATION"
    
    adk web --memory_service_uri=agentengine://AGENT_ENGINE_ID

Replace the following:

  - PROJECT\_ID : Your project ID.
  - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.
  - AGENT\_ENGINE\_ID : The Agent Runtime ID to use for Memory Bank. For example, `456` in `projects/my-project/locations/us-central1/reasoningEngines/456` .

## Interact with your agent

After defining your agent and setting up Memory Bank, you can interact with your agent. If you provided a [callback to trigger memory generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart#memory-generation-callback) when initializing your agent, memories generation will be triggered every time that the agent is invoked.

Memories will be stored using the scope `{"user_id": USER_ID, "app_name": APP_NAME}` corresponding to the user ID and app name used to execute your agent.

The method of interacting with your agent depends on its execution environment:

### Local runner

    # Use `asyncio.run(session_service.create(...))` if you're running this
    # code as a standard Python script.
    session = await session_service.create_session(
        app_name="APP_NAME",
        user_id="USER_ID"
    )
    
    # Use `asyncio.run(call_agent(...))` if you're running this code as a
    # standard Python script.
    await call_agent(
        "Can you fix the temperature?",
        session.id,
        "USER_ID"
    )

Replace the following:

  - APP\_NAME : App name for your runner.
  - USER\_ID : An identifier for your user. Memories generated from this session are keyed by this opaque identifier. The generated memories' scope is stored as `{"user_id": " USER_ID "}` .

### Agent Runtime

When using the ADK template, you can call your Agent Runtime to interact with memory and sessions.

    # Use `asyncio.run(agent_engine.async_create_session(...))` if you're
    # running this code as a standard Python script.
    session = await agent_engine.async_create_session(user_id="USER_ID")
    
    # Use `asyncio.run(call_agent(...))` if you're running this code as a
    # standard Python script.
    await call_agent(
        "Can you fix the temperature?",
        session.get("id"),
        "USER_ID"
    )

Replace the following:

  - USER\_ID : An identifier for your user. Memories generated from this session are keyed by this opaque identifier. The generated memories' scope is stored as `{"user_id": " USER_ID "}` .

### Cloud Run

Refer to the [Testing your agent](https://google.github.io/adk-docs/deploy/gke/#testing-your-agent) section of the ADK Cloud Run deployment documentation.

### GKE

Refer to the [Testing your agent](https://google.github.io/adk-docs/deploy/gke/#testing-your-agent) section of the ADK GKE deployment documentation.

### ADK Web

To use ADK Web, navigate to the local server at `http://localhost:8000` .

By default, ADK Web will set the user ID to `user` . To override the default user ID, include `userId` in the query parameters, like `http://localhost:8000?userId=YOUR_USER_ID` .

For more information, refer to the [ADK Web](https://google.github.io/adk-docs/runtime/web-interface/) page in the ADK documentation.

### Example interaction

**First session**

If you used the `PreloadMemoryTool` , the agent will try to retrieve memories at the beginning of each turn to access preferences the user previously communicated to the agent. During the agent's first interaction with the user, there are no available memories to be retrieved. So, the agent doesn't know any user preferences, such as their preferred temperature, as shown in the following example:

1.  First turn:
    
      - **User** : "Can you fix the temperature?"
    
      - **(Tool Call)** : *ADK tries to fetch memories; no memories are available.*
    
      - **Model** : "What temperature do you prefer?"
    
      - **(Callback)** : *ADK triggers memory generation. No memories are extracted.*

2.  Second turn:
    
      - **User** : I'm comfortable at 71 degrees.
    
      - **(Tool Call)** : *ADK tries to fetch memories; no memories are available.*
    
      - **Model** : Ok, I've updated the temperature to 71 degrees.
    
      - **(Callback)** : *ADK triggers memory generation. Memory "I like the temperature 71 degrees" is created.*

**Second session**

The extracted memory will be available for the next session for the same app name and user ID. If the user provides similar or contradictory information to existing memories, the new information will be [consolidated with the existing memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#understanding_memory_generation) .

1.  First turn
    
      - **User** : Fix the temperature. It's so uncomfortable\!
    
      - **(Tool Call)** : *ADK tries to fetch memories. Memory "I like the temperature 71 degrees" is retrieved.*
    
      - **Model** : Ok, I've updated the temperature to 71 degrees.
    
      - **(Callback)** : *ADK triggers memory generation. No memories are extracted, because the user didn't share anything meaningful to persist.*

2.  Second turn
    
      - **User** : Actually, I prefer it to be warmer in the mornings.
    
      - **(Tool Call)** : *ADK tries to fetch memories. Memory "I like the temperature 71 degrees" is retrieved.*
    
      - **Model** : Ok, I've made the temperature warmer.
    
      - **(Callback)** : *ADK triggers memory generation. The existing memory "I like the temperature 71 degrees" is updated to "I generally like the temperature to be 71 degrees, but I like it to be warmer in the mornings".*

> **Note:** There may be some variance in the agent and Memory Bank's responses depending on what models are used.

## Use a multi-regional Memory Bank with a regional runtime

By default, your agent and Memory Bank are deployed in the same region. However, you can decouple them to use a multi-regional Memory Bank (for example, `us` ) with a regional runtime (for example, `us-central1` ). This configuration lets you maintain a central Memory Bank across different regional deployments.

To use a multi-regional Memory Bank, you must override the default ADK memory service builder to point to the multi-region location and the corresponding Runtime ID.

    import vertexai
    from google.adk.memory import VertexAiMemoryBankService
    from vertexai.agent_engines import AdkApp
    
    # Create the Memory Bank store in a multi-region location (for example, 'us')
    client_mb = vertexai.Client(project="PROJECT_ID", location="us")
    mb_engine = client_mb.agent_engines.create()
    mb_engine_id = mb_engine.api_resource.name.split(\"/\")[-1]
    
    
    # Point your memory service to the 'us' location, 'us' Memory Bank
    def memory_bank_service_builder():
        return VertexAiMemoryBankService(
            project="PROJECT_ID",
            location="us",
            agent_engine_id=mb_engine_id
        )
    
    # Create the AdkApp with the overridden builder
    adk_app = AdkApp(
        agent=agent,
        memory_service_builder=memory_bank_service_builder
    )
    
    # Deploy the runtime to a specific region (for example, 'us-central1')
    client_runtime = vertexai.Client(project="PROJECT_ID", location="us-central1")
    agent_engine = client_runtime.agent_engines.create(
        agent=adk_app,
        config={
            "staging_bucket": "STAGING_BUCKET",
            "requirements": ["google-cloud-aiplatform[agent_engines,adk]"]
        }
    )

Replace the following:

  - PROJECT\_ID : Your project ID.
  - STAGING\_BUCKET : Your Cloud Storage bucket to use for staging your Agent Runtime.

## Clean up

To clean up all resources used in this project, you can [delete the Google Cloud project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) you used for the quickstart.

Otherwise, you can delete the individual resources you created in this tutorial, as follows:

1.  Use the following code sample to delete the Agent Runtime instance, which also deletes any sessions or memories belonging to that runtime.
    
        agent_engine.delete(force=True)

2.  Delete any locally created files.

## What's next

Quickstart

### [Memory Bank API quickstart](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart)

Get started with the Memory Bank API to manage long-term memories.
