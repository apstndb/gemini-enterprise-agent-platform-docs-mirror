---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/optimize-agent
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/optimize/evaluation/optimize-agent
title: Optimize agent prompts
description: Learn how to programmatically optimize agent prompts based on evaluation failure patterns.
data_source: docs.cloud.google.com
---

The *Quality Flywheel* is a continuous cycle of evaluation, analysis, and optimization. You evaluate your agent's performance, analyze the results to identify clusters of failures, and then optimize to address those specific issues. Each iteration improves agent quality.

The Agent Development Kit (ADK) provides an extensible framework for automated agent optimization. Automate agent optimization using the ADK's built-in `adk optimize` command. This command applies the [GEPA algorithm](https://github.com/gepa-ai/gepa) to iteratively refine root system instructions by evaluating them against your test suite.

The framework is extensible: you can implement custom optimization strategies, or develop custom samplers that integrate with your own evaluation pipelines.

For more details on how to get started with optimizing agents using ADK, see [Optimize agents](https://adk.dev/optimize/) in ADK's documentation.
