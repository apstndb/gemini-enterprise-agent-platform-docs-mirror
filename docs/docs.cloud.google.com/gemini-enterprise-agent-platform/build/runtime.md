---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime
title: Agent Runtime
description: Learn about Agent Runtime, a set of services that enables developers to deploy, manage, and scale AI agents in production.
data_source: docs.cloud.google.com
---

> To see an example of getting started with Gemini Enterprise Agent Runtime, run the "Building and Deploying an Agent with Gemini Enterprise Agent Platform" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/intro_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fagent-engine%2Fintro_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fagent-engine%2Fintro_agent_engine.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/intro_agent_engine.ipynb)

**Agent Runtime** is a fully-managed, opinionated runtime that you can use to deploy, operate, and scale agentic applications. Agent Runtime abstracts away the underlying infrastructure, which lets you focus on agent logic instead of operations.

Agent Runtime lets you do the following:

  - [Deploy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) and scale agents with a managed runtime and end-to-end management capabilities.
  - Customize the agent's container image with build-time installation scripts for system dependencies.
  - Use security features including VPC-SC compliance and configuration of authentication and IAM.
  - Access models and tools such as [function calling](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/tools/function-calling) .
  - Deploy agents built using [different Python frameworks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime#supported-frameworks) and the [Agent2Agent open protocol](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-a2a-agent) .

> **Note:** Because the name of Agent Runtime changed over time, the name of the resource in the API reference is [`ReasoningEngine`](https://docs.cloud.google.com/gemini-enterprise-agent-platform/reference/rest/v1/projects.locations.reasoningEngines) to maintain backwards compatibility.

## Create and deploy on Agent Runtime

The workflow for building an agent on Agent Runtime is:

1.  [**Set up the environment**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup) : Set up your Google project and install the latest version of the Agent Platform SDK for Python.
2.  [**Develop an agent**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-agent) : Develop an agent that can be deployed on Agent Runtime.
3.  [**Deploy the agent**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/deploy-an-agent) : Deploy the agent on the Agent Runtime managed runtime.
4.  [**Use the agent**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/use-an-agent) : Query the agent by sending an API request.
5.  [**Manage the deployed agent**](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/manage-deployed-agents) : Manage and delete agents that you have deployed to Agent Runtime.

## Supported frameworks

The following table describes the level of support Agent Runtime provides for various agent frameworks:

| Support level                                                                                                                                                                                                                                                                  | Agent frameworks                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Custom template** : You can adapt a custom template to support deployment to Agent Runtime from your framework. For deploying custom containers, see the [Runtime contract](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/runtime/runtime-contract) . | [CrewAI](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/evaluating_crewai_agent_engine_customized_template.ipynb) , [custom frameworks](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-a-custom-agent)                                                                                                                                                                                          |
| **Agent Platform SDK integration** : Agent Runtime provides managed templates per framework in the Agent Platform SDK and documentation.                                                                                                                                       | [LangChain](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-a-langchain-agent) , [LangGraph](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-a-langgraph-agent) , [AG2](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-ag2-agent) , [LlamaIndex](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-a-llamaindex-agent) |
| **Full integration** : Features are integrated to work across the framework, Agent Runtime, and broader Google Cloud ecosystem.                                                                                                                                                | [Agent Development Kit (ADK)](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/create-an-adk-agent)                                                                                                                                                                                                                                                                                                                                          |

## Deploy in production with Agents CLI

[Video](https://www.youtube.com/watch?v=ECYKo70pPNc)

The [Agents CLI](https://google.github.io/agents-cli/) is the unified command-line interface and skill set for the Gemini Enterprise Agent Platform. It provides coding agents and developers with a predictable path through the Agent Development Lifecycle: scaffold, evaluate, deploy, publish, and observe. The Agents CLI provides the following:

  - **Pre-built agent templates:** ReAct, RAG, multi-agent, and other templates.
  - **Interactive playground** : Test and interact with your agent.
  - **Automated infrastructure** : Uses [Terraform](https://cloud.google.com/docs/terraform) for streamlined resource management.
  - **CI/CD pipelines** : Automated deployment workflows leveraging Cloud Build.
  - **Observability** : Built-in support for Cloud Trace and Cloud Logging.

To get started, see the [Quickstart](https://google.github.io/agents-cli/) .

## Use cases

To learn about Agent Runtime with end-to-end examples, see the following resources:

### Click to expand use cases

Use Case

Description

Links

Build agents by connecting to public APIs

Convert between currencies.  
  
Create a function that connects to a currency exchange app, allowing the model to provide accurate answers to queries such as "What's the exchange rate for euros to dollars today?"

[Agent Platform SDK (Python) notebook - Intro to Building and Deploying an Agent with Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/intro_agent_engine.ipynb)

Designing a community solar project.  
  
Identify potential locations, look up relevant government offices and suppliers, and review satellite images and solar potential of regions and buildings to find the optimal location to install your solar panels.

[Agent Platform SDK (Python) notebook - Building and Deploying a Google Maps API Agent with Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_google_maps_agent.ipynb)

Build agents by connecting to databases

Integration with AlloyDB and Cloud SQL for PostgreSQL.

[Blog post - Announcing LangChain on Gemini Enterprise Agent Platform for AlloyDB and Cloud SQL for PostgreSQL](https://cloud.google.com/blog/products/databases/alloydb-and-cloudsql-for-postgresql-on-langchain-on-vertex-ai)  
  
[Agent Platform SDK (Python) notebook - Deploying a RAG Application with Cloud SQL for PostgreSQL to Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_cloud_sql_pg_rag_agent.ipynb)  
  
[Agent Platform SDK (Python) notebook - Deploying a RAG Application with AlloyDB for PostgreSQL to Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_alloydb_rag_agent.ipynb)

Build agents with tools that access data in your database.

[Agent Platform SDK (Python) notebook - Deploying an Agent with Agent Runtime and MCP Toolbox for Databases](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_mcp_toolbox_for_databases.ipynb)

Query and understand structured datastores using natural language.

[Agent Platform SDK (Python) notebook - Building a Conversational Search Agent with Agent Runtime and RAG on Agent Search](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_vertex_ai_search_rag_agent.ipynb)

Query and understand graph databases using natural language

[Blog post - GenAI GraphRAG and AI agents using Agent Runtime with LangChain and Neo4j](https://www.googlecloudcommunity.com/gc/Cloud-Product-Articles/GenAI-GraphRAG-and-AI-agents-using-Vertex-AI-Reasoning-Engine/ta-p/789066)

Query and understand vector stores using natural language

[Blog post - Simplify GenAI RAG with MongoDB Atlas and Agent Runtime](https://www.mongodb.com/developer/products/atlas/ragdeployment-vertex-ai-reasoning-engine/)

Build agents with Agent Development Kit

Build and deploy agents using Agent Development Kit.

[Agent Development Kit -- Deploy to Agent Runtime](http://google.github.io/adk-docs/deploy/agent-engine)

Build agents with OSS frameworks

Build and deploy agents using the OneTwo open-source framework.

[Blog post - OneTwo and Agent Runtime: exploring advanced AI agent development on Google Cloud](https://www.googlecloudcommunity.com/gc/Community-Blogs/OneTwo-and-Vertex-AI-Reasoning-Engine-exploring-advanced-AI/ba-p/788254)

Build and deploy agents using the LangGraph open-source framework.

[Agent Platform SDK (Python) notebook - Building and Deploying a LangGraph Application with Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tutorial_langgraph.ipynb)

Debugging and optimizing agents

Build and trace agents using OpenTelemetry and Cloud Trace.

[Agent Platform SDK (Python) notebook - Debugging and Optimizing Agents: A Guide to Tracing in Agent Runtime](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/agent-engine/tracing_agents_in_agent_engine.ipynb)

Build multi-agent systems with A2A protocol (preview)

Build interoperable agents that communicate and collaborate with other agents regardless of their framework.

For more information, see the [A2A protocol documentation](https://a2a-protocol.org/) .

## Supported regions

See [Locations](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-locations#supported-regions-agent-engine) for a list of supported regions for Agent Runtime.

## Quota

See [Quota and system limits](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-quotas) for Agent Runtime quota information.

## Pricing

A free tier is available for Agent Runtime. For information about pricing for Agent Runtime, see [Gemini Enterprise Agent Platform pricing](https://cloud.google.com/products/gemini-enterprise-agent-platform/pricing) .

## Migration to the client-based SDK

The `agent_engines` module within the Agent Platform SDK is being refactored to a client-based design for the following key reasons:

  - To align with the [Agent Development Kit](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/adk) (ADK) and Google Gen AI SDK in canonical type representations. This ensures a consistent and standardized way of representing data types across different SDKs, which simplifies interoperability and reduces conversion overhead.
  - For client-level scoping of Google Cloud parameters in multi-project multi-location applications. This allows an application to manage interactions with resources across different Google Cloud projects and geographical locations by configuring each client instance with its specific project and location settings.
  - To improve discoverability and cohesiveness of Agent Runtime services

## What's next

Guide

### [Agent Platform Runtime setup](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/runtime/setup)

Set up your environment to use Agent Platform Runtime.

Resource

### [Get support](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/agent-support)

Get support for Agent Platform development.
