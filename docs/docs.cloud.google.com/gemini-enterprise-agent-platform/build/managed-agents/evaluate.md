---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/evaluate
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/evaluate
title: Evaluate agents built with Managed Agents API on Agent Platform
description: Learn how to evaluate agents built with Managed Agents API on Agent Platform using the Gen AI evaluation service.
data_source: docs.cloud.google.com
---

> This product is a Pre-GA offering, subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , the "Agentic AI Services" terms in the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features may have limited support, and changes to pre-GA products and features may not be compatible with other pre-GA versions. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
> 
> These Pre-GA products are in various stages of internal testing and review. As such, **do not use proprietary, sensitive, or other confidential data with these products** . These products are available to Customers solely for limited testing and evaluation, and you may not use them for commercial or production purposes.

This page describes how to evaluate agents built with [Managed Agents API on Agent Platform](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents) using the Gen AI evaluation service. You can generate synthetic test scenarios, run your agent against them, and score the resulting conversation traces with prebuilt metrics.

> To see an example of evaluating agents built with , run the "Evaluate Managed Agents" notebook in one of the following environments:
> 
> [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-logo-32px.png) Open in Colab](https://colab.research.google.com/github/GoogleCloudPlatform/generative-ai/blob/main/gemini/evaluation/evaluate_managed_agents.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/colab-enterprise-logo-32px.png) Open in Colab Enterprise](https://console.cloud.google.com/agent-platform/colab/import/https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fevaluation%2Fevaluate_managed_agents.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/vertex-ai-workbench-logo-32px.png) Open in Agent Platform Workbench](https://console.cloud.google.com/agent-platform/workbench/deploy-notebook?download_url=https%3A%2F%2Fraw.githubusercontent.com%2FGoogleCloudPlatform%2Fgenerative-ai%2Fmain%2Fgemini%2Fevaluation%2Fevaluate_managed_agents.ipynb) | [![](https://docs.cloud.google.com/static/vertex-ai/images/github-logo-32px.png) View on GitHub](https://github.com/GoogleCloudPlatform/generative-ai/blob/main/gemini/evaluation/evaluate_managed_agents.ipynb)

## Before you begin

1.  Complete the steps in [Create and manage agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage) to create a Managed Agent resource.

2.  Install the Agent Platform SDK with the evaluation extension:
    
        pip install google-cloud-aiplatform[evaluation]

3.  Set up authentication and configure your project:
    
    Replace the following:
    
      - PROJECT\_ID : Your Google Cloud project ID.
    
    <!-- end list -->
    
        import agentplatform
        
        client = agentplatform.Client(
            project="PROJECT_ID",
            location="global",
        )

## Evaluation workflow

Evaluating a Managed Agent follows three steps:

1.  **Generate scenarios** : Automatically create diverse, multi-turn test scenarios from the agent's instructions and tool definitions.
2.  **Run inference** : Execute the agent against the generated scenarios to capture conversation traces.
3.  **Evaluate** : Score the conversation traces using prebuilt metrics.

### Step 1: Generate conversation scenarios

Use `generate_conversation_scenarios` to automatically create test scenarios based on your agent's configuration. The method reads the agent's system instruction and tools to produce realistic user prompts.

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - AGENT\_ID : The ID of your agent resource. For more information on how to retrieve or list custom agents to find their IDs, see [List agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage#list-agents) .

<!-- end list -->

    AGENT_RESOURCE = f"projects/PROJECT_ID/locations/global/agents/AGENT_ID"
    
    scenarios = client.evals.generate_conversation_scenarios(
        agent=AGENT_RESOURCE,
        config={
            "count": 5,
            "generation_instruction": "Generate scenarios where a user asks for a refund.",
        },
    )
    
    scenarios.show()

Each generated scenario includes a `starting_prompt` that represents the initial user message in a conversation.

### Step 2: Run inference

Use `run_inference` to run the agent against the generated scenarios. The agent executes each scenario and produces a conversation trace that captures the full interaction, including tool calls, intermediate steps, and the final response.

    inference_results = client.evals.run_inference(
        agent=AGENT_RESOURCE,
        src=scenarios,
        config={"user_simulator_config": {"max_turn": 5}}
    )
    
    inference_results.show()

### Step 3: Evaluate

Use `evaluate` to score the conversation traces with prebuilt metrics. The following metrics are available for agent evaluation:

| Metric                       | Description                                                                    |
| ---------------------------- | ------------------------------------------------------------------------------ |
| `final_response_quality_v1`  | Evaluates whether the agent successfully completed the user's task.            |
| `safety_v1`                  | Evaluates whether the agent's responses are safe.                              |
| `multi_turn_task_success_v1` | Evaluates whether the agent successfully completed the user's multi-turn task. |

    from agentplatform import types
    
    eval_result = client.evals.evaluate(
        dataset=inference_results,
        metrics=[
            types.RubricMetric.MULTI_TURN_TASK_SUCCESS,
        ],
        agent=AGENT_RESOURCE,
    )
    
    eval_result.show()

The `show()` method displays an interactive report with aggregate scores, per-case rationales, and the agent's conversation traces, including the System Topology (agent tools and instructions).

## Evaluate existing interactions

You can also evaluate interactions that have already been recorded with the agent. This is useful for assessing the quality of production conversations. For information on how to send an interaction to an agent and how to retrieve the interaction\_id, see [Send an interaction to a custom agent](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents#send-custom-agent-interaction) .

Replace the following:

  - PROJECT\_ID : Your Google Cloud project ID.
  - INTERACTION\_ID : The ID of a recorded interaction.
  - AGENT\_RESOURCE : The full resource name of your agent, in the format `projects/PROJECT_ID/locations/global/agents/AGENT_ID` .

<!-- end list -->

    interactions_dataset = types.EvaluationDataset(
        eval_cases=[
            types.EvalCase(
                interactions_data_source=types.InteractionsDataSource(
                    interaction=f"projects/PROJECT_ID/locations/global/interactions/INTERACTION_ID",
                    gemini_agent_config=types.GeminiAgentConfig(
                        gemini_agent=AGENT_RESOURCE,
                    ),
                ),
            ),
        ]
    )
    
    eval_result = client.evals.evaluate(
        dataset=interactions_dataset,
        metrics=[
            types.RubricMetric.MULTI_TURN_TASK_SUCCESS,
        ],
        agent=AGENT_RESOURCE,
    )
    
    eval_result.show()

## What's next

Guide

### [Create and manage agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/create-manage)

Learn how to create, update, list, get, and delete agents using the REST API.

Guide

### [Interact with agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/build/managed-agents/interact-with-agents)

Learn how to interact with agents at runtime, manage session state, and dynamically override configurations.

Overview

### [Agent evaluation](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/agent-evaluation)

Learn about agent evaluation in Google Agent Platform.

Guide

### [Manage evaluation metrics](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/manage-metrics)

Learn how to manage evaluation metrics in Google Agent Platform.
