---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart
title: Agent Platform Memory Bank API quickstart
description: Learn how to make API calls directly to Sessions and Agent Platform Memory Bank using the Agent Platform SDK to manage sessions and long-term memories.
data_source: docs.cloud.google.com
---

You can use the Agent Platform SDK to make API calls directly to Memory Bank. Use the Agent Platform SDK if you don't want an agent framework to orchestrate calls for you, or you want to integrate Memory Bank with agent frameworks other than Agent Development Kit (ADK).

This document shows how to create, upload, retrieve, and remove memories using API calls.

For the quickstart using ADK, see [Memory Bank quickstart with ADK](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart) .

> To see an example of using with the SDK, run the "Get started with Memory Bank" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Fmemory_bank%2Fget_started_with_memory_bank.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/memory_bank/get_started_with_memory_bank.ipynb)

> To see an example of using with LangGraph, run the "Get started with - LangGraph" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/memory/get_started_with_memory_bank_langgraph.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fagent-engine%2Fmemory%2Fget_started_with_memory_bank_langgraph.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fagent-engine%2Fmemory%2Fget_started_with_memory_bank_langgraph.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/memory/get_started_with_memory_bank_langgraph.ipynb)

## Before you begin

To complete the steps demonstrated in this tutorial, you must first follow the steps in [Set up for Memory Bank](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup) . Before you begin this quickstart, ensure that you have created a Memory Bank instance and a Sessions instance, as shown in the following example:

    import vertexai
    
    client = vertexai.Client(
      project="PROJECT_ID",
      location="LOCATION"
    )
    
    memory_bank = client.agent_engines.create()
    sessions = client.agent_engines.create()

## Generate memories with Agent Platform Sessions

After setting up Agent Platform Sessions, you can create sessions and append events to them. Then, you can use Memory Bank to generate memories from the user's conversation with the agent so that the memories are available for future user interactions. For more information, see [Generate memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) and [Fetch memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories) .

> **Note:** You can also provide the conversation history directly in the `GenerateMemories` payload using [direct contents source](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#json-format) .

1.  Create a session with an opaque user ID. Any memories generated from this session are automatically keyed by the scope `{"user_id": " USER_ID "}` unless you explicitly provide a scope when generating memories.
    
        import vertexai
        
        client = vertexai.Client(
        project="PROJECT_ID",
        location="LOCATION"
        )
        
        session = client.agent_engines.sessions.create(
        # The name can be fetched using `sessions.api_resource.name`.
        name="SESSIONS_NAME",
        user_id="USER_ID"
        )
    
    Replace the following:
    
      - PROJECT\_ID : Your project ID.
    
      - LOCATION : Your region. See the [supported regions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations) for Memory Bank.
    
      - SESSIONS\_NAME : The name of the Sessions instance that you created or an existing Sessions instance. The name should be in the following format: `projects/{your project}/locations/{your location}/reasoningEngine/{your reasoning engine}` .
    
      - USER\_ID : An identifier for your user. Any memories generated from this session are automatically keyed by the scope `{"user_id": " USER_ID "}` unless you explicitly provide a scope when generating memories.

2.  Iteratively upload events to your session. Events can include any interactions between your user, agent, and tools. The ordered list of events represents your session's conversation history. This conversation history is used as the source material for generating memories for that particular user.
    
        import datetime
        
        client.agent_engines.sessions.events.append(
        name=session.response.name,
        author="user",  # Required by Sessions.
        invocation_id="1",  # Required by Sessions.
        timestamp=datetime.datetime.now(tz=datetime.timezone.utc),  # Required by Sessions.
        config={
          "content": {
            "role": "user",
            "parts": [{"text": "hello"}]
          }
        }
        )

3.  To generate memories from your conversation history, trigger a memory generation request for the session:
    
        client.agent_engines.memories.generate(
          name=memory_bank.api_resource.name,
          vertex_session_source={
            # `session` should have the format "projects/.../locations/.../reasoningEngines/.../sessions/...".
            "session": session.response.name
          },
          # Optional when using Sessions. Defaults to {"user_id": session.user_id}.
          scope=SCOPE
        )

Replace the following:

  - (Optional) SCOPE : A dictionary representing the scope of the generated memories, with a maximum of 5 key value pairs and no `*` characters. For example, `{"session_id": "MY_SESSION"}` . Only memories with the same scope are considered for consolidation. If not provided, `{"user_id": session.user_id}` is used.

## Upload memories

As an alternative to [generating memories using raw dialogue](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) , you can upload memories or have your agents add them directly using [`GenerateMemories` with pre-extracted facts](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#consolidate-pre-extracted-memories) . Rather than Memory Bank extracting information from your content, you provide the facts that should be stored about your user directly.

To ensure consistency with [generated memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/api-quickstart#generate-memories) , try to write pre-extracted facts in the same perspective that you've [configured for the given scope](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#memory-perspective) . By default, memories are generated in the first-person perspective (for example, `I am a software engineer` ).

    client.agent_engines.memories.generate(
        name=memory_bank.api_resource.name,
        direct_memories_source={"direct_memories": [{"fact": "FACT"}]},
        scope=SCOPE
    )

Replace the following:

  - FACT : The pre-extracted fact that should be consolidated with existing memories. You can provide up to 5 pre-extracted facts in a list like the following:
    
        {"direct_memories": [{"fact": "fact 1"}, {"fact": "fact 2"}]}

  - SCOPE : A dictionary, representing the scope of the generated memories. For example, `{"session_id": "MY_SESSION"}` . Only memories with the same scope are considered for consolidation.

Alternatively, you can use `CreateMemory` to upload memories without using Memory Bank for either memory extraction or consolidation.

> **Caution:** Memories uploaded using `CreateMemory` won't be consolidated with existing memories, so you can end up with duplicated memories for the same scope. Created memories are available for similarity search and can be consolidated for future requests when [generating memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) .

    memory = client.agent_engines.memories.create(
        name=memory_bank.api_resource.name,
        fact="This is a fact.",
        scope={"user_id": "123"}
    )
    
    """
    Returns an AgentEngineMemoryOperation containing the created Memory like:
    
    AgentEngineMemoryOperation(
      done=True,
      metadata={
        "@type': 'type.googleapis.com/google.cloud.aiplatform.v1beta1.CreateMemoryOperationMetadata",
        "genericMetadata": {
          "createTime": '2025-06-26T01:15:29.027360Z',
          "updateTime": '2025-06-26T01:15:29.027360Z'
        }
      },
      name="projects/.../locations/us-central1/reasoningEngines/.../memories/.../operations/...",
      response=Memory(
        create_time=datetime.datetime(2025, 6, 26, 1, 15, 29, 27360, tzinfo=TzInfo(UTC)),
        fact="This is a fact.",
        name="projects/.../locations/us-central1/reasoningEngines/.../memories/...",
        scope={
          "user_id": "123"
        },
        update_time=datetime.datetime(2025, 6, 26, 1, 15, 29, 27360, tzinfo=TzInfo(UTC))
      )
    )
    """

## Retrieve and use memories

You can retrieve memories for your user and include them in your system instructions to give the LLM access to your personalized context.

For more information about retrieving memories using a scope-based method, see [Fetch memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#scope-based) .

    # Retrieve all memories for User ID 123.
    retrieved_memories = list(
        client.agent_engines.memories.retrieve(
            name=memory_bank.api_resource.name,
            scope={"user_id": "123"}
        )
    )

You can use `jinja` to convert your structured memories into a prompt:

    from jinja2 import Template
    
    template = Template("""
    <MEMORIES>
    Here is some information about the user:
    {% for retrieved_memory in data %}* {{ retrieved_memory.memory.fact }}
    {% endfor %}</MEMORIES>
    """)
    
    prompt = template.render(data=retrieved_memories)
    
    """
    Output:
    
    <MEMORIES>
    Here is some information about the user:
    * This is a fact
    </MEMORIES>
    """

## Remove memories

There are multiple ways to delete memories from your Memory Bank instance depending on how you want to select which memories should be removed.

### Remove by resource name

If you know exactly which memory resource you want to remove, you can delete a specific memory using its resource name:

    client.agent_engines.memories.delete(
        name=MEMORY_NAME,
        config={
            # Set to false (default) if you want to delete the memory asynchronously.
            "wait_for_completion": True
        }
    )

Replace the following:

  - MEMORY\_NAME : The name of the Memory to delete. The name should be in the following format: `projects/{your project}/locations/{your location}/reasoningEngine/{your reasoning engine}/memories/{your memory}` . You can find the Memory name by [fetching memories](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories) .

### Remove by criteria

You can use criteria-based deletion to remove one or more memories. Only memories that match the provided filters will be deleted. You must specify at least one of `filter` (applied to system fields) or `filter_groups` (applied to metadata fields).

    operation = client.agent_engines.memories.purge(
        name=memory_bank.api_resource.name,
        # Specify at least one of `filter` or `filter_groups`.
        filter="FILTER_STRING",
        filter_groups=FILTER_GROUPS,
        # Set to false (default) if you want to stage but not execute the purge operation.
        force=True,
        config={
            # Set to false (default) if you want to purge memories asynchronously.
            "wait_for_completion": True
        }
    )

Replace the following:

  - FILTER\_STRING : A string using [EBNF](https://google.aip.dev/assets/misc/ebnf-filtering.txt) syntax for filtering against system fields. System fields include `create_time` , `update_time` , `fact` , and [`topics`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#topic-filter) . For more information about filtering against system fields, see the [Filter by metadata fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#system-filter) section on the Fetch memories page.
  - FILTER\_GROUPS : A list of dictionaries or objects for filtering against memory metadata. For more information about filtering against metadata fields, see the [Filter by system fields](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/fetch-memories#metadata-filter) section on the Fetch memories page.

The operation will return a count of how many memories were purged (if `force=True` ) or would be purged if the operation was executed (if `force=False` ).

    print(operation.response.purge_count)

For example, you can purge all memories that belong to a scope for `user_id` "123":

    operation = client.agent_engines.memories.purge(
        name=memory_bank.api_resource.name,
        filter="scope.user_id=\"123\""
        force=True
    )

### Remove by semantic meaning

> **Note:** Expected behavior may vary depending on what [memory topics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#configure-memory-topics) and [few-shot examples](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/setup#configure-few-shots) you have configured.

During [memory generation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories) , Memory Bank will decide whether to create, update, or delete memories based on the content of the newly extracted information and the existing memories. A memory may be deleted if the new information contradicts it or if the extracted content instructs Memory Bank to forget a subject (in the case of the [`EXPLICIT_INSTRUCTIONS` memory topic](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/generate-memories#memory-topics) ).

For example, the following request would delete existing memories that contain information about dietary preferences, if they exist for the given `scope` :

    from google import genai
    
    client.agent_engines.memories.generate(
        name=memory_bank.api_resource.name,
        direct_contents_source={
          "events": [{
            "content": genai.types.Content(
              role="user",
              parts=[
                genai.types.Part.from_text(text="Forget my dietary preferences.")
              ]
            )
          }]
        },
        scope={...}
    )

## Clean up

To clean up all resources used in this project, you can [delete the Google Cloud project](https://docs.cloud.google.com/resource-manager/docs/creating-managing-projects#shutting_down_projects) you used for the quickstart.

Otherwise, you can delete the individual resources you created in this tutorial, as follows:

1.  Use the following code sample to delete the Agent Platform instance, which also deletes any sessions or memories associated with the Agent Platform instance.
    
        agent_engine.delete(force=True)

2.  Delete any locally created files.

## What's next

Quickstart

### [Quickstart with Agent Development Kit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/memory-bank/adk-quickstart)

Get started with the Agent Development Kit (ADK).
