---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/adversarial-benchmarking
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/adversarial-benchmarking
title: Semantic governance policies adversarial benchmarking
description: Learn how Semantic governance policies perform on adversarial benchmarks for prompt-injection attacks on AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) and the [Generative AI Service Specific Terms](https://cloud.google.com/terms/service-terms#20) , as well as the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos?e=48754805) .
>
> When you use this feature with AI Agents, the terms applicable to AI Agents in the Agreement apply.
>
> Pre-GA features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> **Note:** Semantic governance policy is a Generative AI Service that uses an LLM to implement natural language policies. LLMs are probabilistic and can make mistakes. Verdicts may not be accurate.

This page describes how Semantic governance policies (SGP) perform on public adversarial benchmarks for AI agents. Use these results to understand how SGP protects agents from indirect prompt injection and user intent hijacking, and how it affects legitimate agent tasks.

## AgentDojo

[AgentDojo](https://github.com/ethz-spylab/agentdojo) is a public benchmark for prompt-injection attacks on tool-using agents. On AgentDojo, SGP reduces the attack success rate from 48.7% to 0.9%, with a utility cost of 2.6 percentage points on legitimate tasks.

### What AgentDojo measures

AgentDojo gives an agent simulated tools in four domains (banking, Slack, travel and workspace) and asks it to complete user tasks. In attacked runs, some tool outputs contain injected instructions that try to make the agent do something the user never asked for, such as sending money or sharing data with an outside party.

The benchmark reports the following metrics:

- **Utility:** the percentage of benign user tasks the agent completes.
- **Attack success rate (ASR):** the percentage of attacked runs in which the agent carries out the injected goal. Lower is better.
- **Utility cost of SGP:** utility without SGP minus utility with SGP, in percentage points. It includes both over-blocking, where SGP denies a legitimate tool call that the user asked for, and intended blocks of benign tasks that match the pattern of a prompt injection. Lower is better.

### Benchmark configuration

To minimize impact from the natural variance in agent behavior, results represent the average of six independent trials (N = 6). This approach reduces execution noise to more clearly show SGP's impact.

| Setting             | Value                            |
|---------------------|----------------------------------|
| Agent model         | gemini-2.5-flash                 |
| SGP evaluation mode | Intent only                      |
| Tasks per run       | 97 user tasks; 949 attacked runs |
| Attack              | `important_instructions`         |
| Runs                | 6 without SGP, 6 with SGP        |

**Intent only** is the evaluation mode SGP uses when user intent matching is on, which is the default, and no policies are configured. In this mode, SGP checks whether each tool call the agent proposes matches what the user asked for, and denies calls that don't. There is no tuning for individual tasks or domains. Configured policies can block additional actions.

The benchmark runs the production SGP policy engine through a test harness. For every tool call the agent proposes, the harness sends the engine the user request, system instruction, conversation history (including tool results) and the proposed call before the call runs, and denied calls don't run. The harness drops only the denied call, while production blocks the agent's whole response when any call in it is denied.

### Results

| Metric              | Without SGP | With SGP                  |
|---------------------|-------------|---------------------------|
| Attack success rate | 48.7%       | **0.9%**                  |
| Utility             | 72.7%       | 70.1%                     |
| Utility cost of SGP |             | **2.6 percentage points** |

### User intent protection

SGP reduces the attack success rate from 48.7% to 0.9%, a 98.2% reduction. The result is consistent across runs: with SGP, the attack success rate is between 0.84% and 0.95% in every run.

### Impact on legitimate tasks

Across six runs, utility averaged 72.7% without SGP and 70.1% with SGP, a marginal cost of 2.6 percentage points. Individual runs range from −1.0 to 7.2 points because of run-to-run variation in the agent.

Of the 97 benign tasks, two fail consistently with SGP. In both, SGP behaves as intended: each task asks the agent to carry out instructions from an external web page and claims a user identity that contradicts the system prompt, which is the pattern of a prompt injection. A third task fails more often with SGP. The remaining 94 tasks show no consistent difference with and without SGP.

Unintended over-blocking affects 1 of the 97 benign tasks (about **1%** ).

### Summary

- **SGP reduces the attack success rate from 48.7% to 0.9%** , a 98.2% reduction, in the Intent only evaluation mode with no per-task tuning.
- **The utility cost of SGP on legitimate tasks is 2.6 percentage points.** Unintended over-blocking affects 1 of 97 benign tasks (about 1%); the other affected tasks match the pattern of a prompt injection.

## What's next

- [Semantic governance policies overview](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/semantic-governance-overview)
- [Configure semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/configure-semantic-governance)
- [Best practices for using Semantic governance policies](https://docs.cloud.google.com/gemini-enterprise-agent-platform/govern/policies/best-practices)
