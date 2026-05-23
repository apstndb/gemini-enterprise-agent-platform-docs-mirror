---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent
title: Create an Agent2Agent agent
description: Learn how to develop and test Agent2Agent (A2A) agents locally on Agent Runtime.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

Agent Runtime lets you develop and deploy agents using the Agent2Agent (A2A) protocol. A2A is an open standard designed to enable seamless communication and collaboration between AI agents.

This document explains how to develop and test an A2A agent locally, including defining components like `AgentCard` and `AgentExecutor` .

For more information on managing your deployed agents, see [Manage deployed agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents) .

> To see an example of Get started with A2A on Agent Platform Runtime, run the "Get started with A2A on Agent Platform Runtime" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/tutorial_a2a_on_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Ftutorial_a2a_on_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fagents%2Fagent_engine%2Ftutorial_a2a_on_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/agents/agent_engine/tutorial_a2a_on_agent_engine.ipynb)

The core workflow involves the following steps:

1.  [Define key components](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent#define_agent_components)
2.  [Create local agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent#create_a_local_agent)
3.  [Test the local agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent#test_the_local_agent)

## Define agent components

To create an A2A agent, you need to define the following components: an `AgentCard` , an `AgentExecutor` , and an ADK `LlmAgent` .

  - `AgentCard` contains a metadata document that describes your agent's capabilities. `AgentCard` is like a business card that other agents can use to discover what your agent can do. For more details, see the [Agent Card specification](https://a2a-protocol.org/dev/specification/agent-card/) .
  - `AgentExecutor` contains the agent's core logic and defines how it handles tasks. This is where you implement the agent's behavior. You can read more about it in the [A2A protocol specification](https://a2a-protocol.org/dev/specification/) .
  - Optional: `LlmAgent` defines the ADK agent, including its system instructions, generative model, and tools.

### Define an `AgentCard`

The following code sample defines an `AgentCard` for a currency exchange rate agent:

    from a2a.types import AgentCard, AgentSkill
    from vertexai.preview.reasoning_engines.templates.a2a import create_agent_card
    
    # Define the skill for the CurrencyAgent
    currency_skill = AgentSkill(
        id='get_exchange_rate',
        name='Get Currency Exchange Rate',
        description='Retrieves the exchange rate between two currencies on a specified date.',
        tags=['Finance', 'Currency', 'Exchange Rate'],
        examples=[
            'What is the exchange rate from USD to EUR?',
            'How many Japanese Yen is 1 US dollar worth today?',
        ],
    )
    
    # Create the agent card using the utility function
    agent_card = create_agent_card(
        agent_name='Currency Exchange Agent',
        description='An agent that can provide currency exchange rates',
        skills=[currency_skill]
    )

### Define an `AgentExecutor`

The following code example defines an `AgentExecutor` that responds with the currency exchange rate. It takes a `CurrencyAgent` instance and initializes the ADK Runner to execute requests.

    import requests
    from a2a.server.agent_execution import AgentExecutor, RequestContext
    from a2a.server.events import EventQueue
    from a2a.server.tasks import TaskUpdater
    from a2a.types import TaskState, TextPart, UnsupportedOperationError, Part
    from a2a.utils import new_agent_text_message
    from a2a.utils.errors import ServerError
    from google.adk import Runner
    from google.adk.agents import LlmAgent
    from google.adk.artifacts import InMemoryArtifactService
    from google.adk.memory.in_memory_memory_service import InMemoryMemoryService
    from google.adk.sessions import InMemorySessionService
    from google.genai import types
    
    class CurrencyAgentExecutorWithRunner(AgentExecutor):
        """Executor that takes an LlmAgent instance and initializes the ADK Runner internally."""
    
        def __init__(self, agent: LlmAgent):
            self.agent = agent
            self.runner = None
    
        def _init_adk(self):
            if not self.runner:
                self.runner = Runner(
                    app_name=self.agent.name,
                    agent=self.agent,
                    artifact_service=InMemoryArtifactService(),
                    session_service=InMemorySessionService(),
                    memory_service=InMemoryMemoryService(),
                )
    
        async def cancel(self, context: RequestContext, event_queue: EventQueue):
            raise ServerError(error=UnsupportedOperationError())
    
        async def execute(
            self,
            context: RequestContext,
            event_queue: EventQueue,
        ) -> None:
            self._init_adk() # Initialize on first execute call
    
            if not context.message:
                return
    
            user_id = context.message.metadata.get('user_id') if context.message and context.message.metadata else 'a2a_user'
    
            updater = TaskUpdater(event_queue, context.task_id, context.context_id)
            if not context.current_task:
                await updater.submit()
            await updater.start_work()
    
            query = context.get_user_input()
            content = types.Content(role='user', parts=[types.Part(text=query)])
    
            try:
                session = await self.runner.session_service.get_session(
                    app_name=self.runner.app_name,
                    user_id=user_id,
                    session_id=context.context_id,
                ) or await self.runner.session_service.create_session(
                    app_name=self.runner.app_name,
                    user_id=user_id,
                    session_id=context.context_id,
                )
    
                final_event = None
                async for event in self.runner.run_async(
                    session_id=session.id,
                    user_id=user_id,
                    new_message=content
                ):
                    if event.is_final_response():
                        final_event = event
    
                if final_event and final_event.content and final_event.content.parts:
                    response_text = "".join(
                        part.text for part in final_event.content.parts if hasattr(part, 'text') and part.text
                    )
                    if response_text:
                        await updater.add_artifact(
                            [TextPart(text=response_text)],
                            name='result',
                        )
                        await updater.complete()
                        return
    
                await updater.update_status(
                    TaskState.failed,
                    message=new_agent_text_message('Failed to generate a final response with text content.'),
                    final=True
                )
    
            except Exception as e:
                await updater.update_status(
                    TaskState.failed,
                    message=new_agent_text_message(f"An error occurred: {str(e)}"),
                    final=True,
                )

### Define an `LlmAgent`

First, define a currency exchange tool for the `LlmAgent` to use:

    def get_exchange_rate(
        currency_from: str = "USD",
        currency_to: str = "EUR",
        currency_date: str = "latest",
    ):
        """Retrieves the exchange rate between two currencies on a specified date.
        Uses the Frankfurter API (https://api.frankfurter.app/) to obtain
        exchange rate data.
        """
        try:
            response = requests.get(
                f"https://api.frankfurter.app/{currency_date}",
                params={"from": currency_from, "to": currency_to},
            )
            response.raise_for_status()
            return response.json()
        except requests.exceptions.RequestException as e:
            return {"error": str(e)}

Then, define an ADK `LlmAgent` that uses the tool.

    my_llm_agent = LlmAgent(
        model='gemini-2.0-flash',
        name='currency_exchange_agent',
        description='An agent that can provide currency exchange rates.',
        instruction="""You are a helpful currency exchange assistant.
                       Use the get_exchange_rate tool to answer user questions.
                       If the tool returns an error, inform the user about the error.""",
        tools=[get_exchange_rate],
    )

## Create a local agent

Once you have defined your agent's components, create an instance of the [`A2aAgent`](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.A2aAgent) class that uses the `AgentCard` , `AgentExecutor` , and `LlmAgent` to begin local testing.

    from vertexai.preview.reasoning_engines import A2aAgent
    
    a2a_agent = A2aAgent(
        agent_card=agent_card, # Assuming agent_card is defined
        agent_executor_builder=lambda: CurrencyAgentExecutorWithRunner(
            agent=my_llm_agent,
        )
    )
    a2a_agent.set_up()

The A2A Agent template helps you create an A2A-compliant service. The service acts as a wrapper, abstracting away the converting layer from you.

## Test the local agent

The currency exchange rate agent supports the following three methods:

  - `handle_authenticated_agent_card`
  - `on_message_send`
  - `on_get_task`

### Test `handle_authenticated_agent_card`

The following code retrieves the agent's authenticated card, which describes the agent's capabilities.

    # Test the `authenticated_agent_card` endpoint.
    response_get_card = await a2a_agent.handle_authenticated_agent_card(request=None, context=None)
    print(response_get_card)

### Test `on_message_send`

The following code simulates a client sending a new message to the agent. The [`A2aAgent`](https://docs.cloud.google.com/python/docs/reference/vertexai/latest/vertexai.preview.reasoning_engines.A2aAgent) creates a new task and returns the task's ID.

    import json
    from starlette.requests import Request
    import asyncio
    
    # 1. Define the message payload you want to send.
    message_data = {
        "message": {
            "messageId": "local-test-message-id",
            "content":[
                  {
                      "text": "What is the exchange rate from USD to EUR today?"
                  }
              ],
            "role": "ROLE_USER",
        },
    }
    
    # 2. Construct the request
    scope = {
        "type": "http",
        "http_version": "1.1",
        "method": "POST",
        "headers": [(b"content-type", b"application/json")],
    }
    
    async def receive():
        byte_data = json.dumps(message_data).encode("utf-8")
        return {"type": "http.request", "body": byte_data, "more_body": False}
    
    post_request = Request(scope, receive=receive)
    
    # 3. Call the agent
    send_message_response = await a2a_agent.on_message_send(request=post_request, context=None)
    
    print(send_message_response)

### Test `on_get_task`

The following code retrieves the status and the result of a task. The output shows that the task is completed and includes the "Hello World" response artifact.

    from starlette.requests import Request
    import asyncio
    
    # 1. Provide the task_id from the previous step.
    # In a real application, you would store and retrieve this ID.
    task_id_to_get = send_message_response['task']['id']
    
    # 2. Define the path parameters for the request.
    task_data = {"id": task_id_to_get}
    
    # 3. Construct the starlette.requests.Request object directly.
    scope = {
        "type": "http",
        "http_version": "1.1",
        "method": "GET",
        "headers": [],
        "query_string": b'',
        "path_params": task_data,
    }
    
    async def empty_receive():
        return {"type": "http.disconnect"}
    
    get_request = Request(scope, empty_receive)
    
    # 4. Call the agent's handler to get the task status.
    task_status_response = await a2a_agent.on_get_task(request=get_request, context=None)
    
    print(f"Successfully retrieved status for Task ID: {task_id_to_get}")
    print("\nFull task status response:")
    print(task_status_response)

## What's next

Guide

### [Deploy agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent)

Learn the five ways to deploy an agent on Agent Platform Runtime based on your development needs.

Guide

### [Use an Agent2Agent agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-a2a-agent)

Use an Agent2Agent agent with Agent Platform Runtime.

Guide

### [Evaluate your agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/evaluate-agents)

Create and deploy a basic agent and use the Gen AI evaluation service to evaluate the agent

Troubleshooting

### [Troubleshoot agent creation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/troubleshooting/agent-creation)

Learn how to resolve common errors when creating custom agents.

Resource

### [Get support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support)

Find resources and support for Google Agent Platform.

Resource

### [Agent2Agent samples repository](https://github.com/a2aproject/a2a-samples/tree/main/samples/python/agents)

Explore Agent2Agent samples in Python on GitHub.
