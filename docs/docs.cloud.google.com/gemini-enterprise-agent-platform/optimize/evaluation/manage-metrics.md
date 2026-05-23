---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/manage-metrics
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/manage-metrics
title: Manage evaluation metrics
description: Manage evaluation metrics in the Metric Registry to define and reuse performance standards for your agents.
data_source: docs.cloud.google.com
---

> **Preview - Agent evaluation on Gemini Enterprise Agent Platform**
> 
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) as well as the [Generative AI Service Specific Terms](https://cloud.google.com/terms/service-terms#20) . This feature allows customers to evaluate AI Agents, and so the "Agentic AI Services" Service Specific Terms apply. Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

## Before you begin

Before you manage evaluation metrics, ensure you have the following:

  - A Google Cloud project with the **Agent Platform API** enabled.
  - (Optional) If using the **Agent Platform SDK** , initialize the client as described in [Evaluate your agents](https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/evaluate-agents) .

The **Metric Registry** allows you to define, store, and manage reusable configurations for how your agents are evaluated. Instead of configuring criteria for every test run, you can save standardized metrics—such as a custom LLM-based rubric for safety or a Python function for execution accuracy—and apply them consistently to both offline assessments and continuous online monitors.

## Metric types

Agent Platform supports three types of metrics in the registry:

  - **Predefined Metrics:** Managed metrics provided by Google, including multi-turn raters for task success, tool use quality, and trajectory compliance.
  - **Custom LLM Metrics:** Natural language rubrics where a "Judge LLM" evaluates an agent's response based on your specific criteria and rating scales.
  - **Custom Code Metrics:** Python functions that programmatically validate agent behavior, such as checking for a specific output format or verifying a tool response.

In addition to managed metrics provided by Google, you can use customized registered metrics for evaluation.

## Predefined metrics

Agent Platform provides a set of predefined metrics for evaluating agents. These metrics are managed by Google and cover common evaluation dimensions for both single-turn and multi-turn agent interactions.

You can access predefined metrics in the SDK using `types.RubricMetric.METRIC_NAME` . For the full details of all managed rubric-based metrics, including input requirements and output formats, see [Details for managed rubric-based metrics](https://docs.cloud.google.com/vertex-ai/generative-ai/docs/models/rubric-metric-details#managed-metrics-details) .

### Single-turn agent metrics

The following metrics evaluate a single agent interaction (one prompt and one response, potentially with intermediate tool calls):

| Metric                           | Type            | SDK accessor                                | Description                                                                                                                                                                                                |
| -------------------------------- | --------------- | ------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Agent Final Response Quality** | Adaptive rubric | `types.RubricMetric.FINAL_RESPONSE_QUALITY` | Comprehensive evaluation that auto-generates rubric criteria based on the agent's configuration (system instructions and tool declarations) and the user's prompt.                                         |
| **Agent Hallucination**          | Static rubric   | `types.RubricMetric.HALLUCINATION`          | Checks factuality by segmenting the response into atomic claims and verifying each claim is grounded in the tool usage from intermediate events.                                                           |
| **Agent Tool Use Quality**       | Adaptive rubric | `types.RubricMetric.TOOL_USE_QUALITY`       | Evaluates the selection of appropriate tools, correct parameter usage, and adherence to the specified sequence of operations.                                                                              |
| **Safety**                       | Static rubric   | `types.RubricMetric.SAFETY`                 | Assesses whether the response violates safety policies, including PII and demographic data, hate speech, dangerous content, harassment, or sexually explicit content. Returns 1 for safe and 0 for unsafe. |

### Multi-turn agent metrics

The following metrics evaluate multi-turn agent conversations. They analyze the full conversation context to assess overall agent performance across multiple turns:

| Metric                                  | Type            | SDK accessor                                       | Description                                                                                                                                                                                    |
| --------------------------------------- | --------------- | -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Agent Multi-turn Task Success**       | Adaptive rubric | `types.RubricMetric.MULTI_TURN_TASK_SUCCESS`       | Evaluates whether the agent successfully achieved the goal or goals of the conversation. This reference-free metric focuses on *whether* the goal was achieved, not *how* it was achieved.     |
| **Agent Multi-turn Tool Use Quality**   | Adaptive rubric | `types.RubricMetric.MULTI_TURN_TOOL_USE_QUALITY`   | Evaluates the quality of function calls made during a multi-turn conversation. Assesses whether the agent called the right tools with correct arguments at the right time.                     |
| **Agent Multi-turn Trajectory Quality** | Adaptive rubric | `types.RubricMetric.MULTI_TURN_TRAJECTORY_QUALITY` | Evaluates the overall trajectory (path) of the conversation. Unlike Task Success, this metric assesses *how* the agent achieved the goal—whether the reasoning path was logical and efficient. |

### Use predefined metrics in the SDK

    from vertexai import evals, types
    
    # Run an evaluation with predefined metrics
    result = client.evals.evaluate(
        dataset=eval_dataset,
        metrics=[
            types.RubricMetric.FINAL_RESPONSE_QUALITY,
            types.RubricMetric.TOOL_USE_QUALITY,
            types.RubricMetric.HALLUCINATION,
            types.RubricMetric.SAFETY,
        ],
    )
    
    # Visualize results in Colab
    result.show()

## Manage metrics in the console

1.  In the Google Cloud console, navigate to the **Agent Platform \> Agents \> Evaluation** page.

2.  Click the **Metrics** tab to view the registry.

3.  **Create a metric:** Click **New metric** and select **Custom LLM metric** or **Custom code metric** .

4.  **Define rubrics:** For LLM metrics, use the **Sample** buttons to quickly populate instructions, criteria (for example, **Clarity** or **Excitement** ), and rating scores.

5.  **View and edit:** Click any metric name to view its definition in read-only mode, or use the **More options** *more\_vert* icon to **Duplicate** or **Delete** the resource.

## Manage metrics with the SDK

You can programmatically register and use metrics using the **Agent Platform SDK** .

### Register a Custom LLM Metric

    from vertexai import evals, types
    
    # Define a metric with a specific rubric
    tone_check_metric = types.LLMMetric(
            name="tone_check",
            prompt_template="Analyze the tone of the response ...",
            result_parsing_function="""
              import json, re
              def parse_results(responses):
                  response = json.loads(responses[0])
                  return {"score": response.get("score", 0.0),
                          "explanation": response.get("explanation", "default explanation")}
              """
    )
    
    # Register the custom metric
    tone_check_metric_path = client.evals.create_evaluation_metric(
        metric=tone_check_metric
    )

### Register a Custom Code Metric

    from vertexai import evals, types
    
    # Define a metric with custom python code
    accuracy_metric_code = """
    def evaluate(instance: dict) -> float:
        agent_data = instance.get('agent_eval_data', {})
        turns = agent_data.get('turns', [])
        for turn in turns:
            ...
    """
    
    accuracy_metric = types.CodeExecutionMetric(
        name="multi_turn_accuracy",
        custom_function=accuracy_metric_code
    )
    
    # Register the custom metric
    accuracy_metric_path = client.evals.create_evaluation_metric(
        metric=accuracy_metric
    )
