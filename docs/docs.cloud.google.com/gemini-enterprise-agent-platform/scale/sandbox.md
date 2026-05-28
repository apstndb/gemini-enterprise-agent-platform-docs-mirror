---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox
title: Sandboxes overview
description: Overview of Sandboxes in Gemini Enterprise Agent Platform.
data_source: docs.cloud.google.com
---

Many agent tasks involve executing untrusted code or interacting with external environments in ways that could pose security risks. The Gemini Enterprise Agent Platform provides isolated **sandboxes** to handle these workloads securely.

Sandboxes provide secure, isolated compute environments that are spawned to perform specific tasks on behalf of an agent. By running these operations in a sandbox, you can protect your infrastructure and data from potentially malicious or erroneous actions performed by the agent. Sandboxes mitigate these risks by:

  - **Isolation** : Each sandbox is isolated from other sandboxes and the host system. Actions taken by one agent in a sandbox doesn't affect other agents or users sharing the same runtime resources.
  - **Security** : Operations within the sandbox are restricted, preventing unauthorized access to your resources. All sandbox environments use secure container sandboxing, providing a strong security boundary. Malicious code can't access sensitive data or credentials within the runtime.
  - **Safety** : If an agent executes a harmful command or infinite loop, the impact is contained within the sandbox. For example, poorly written or malicious code could consume all available CPU or memory.

## Sandbox compared to runtime

The agent runtime and a sandbox differ in their purpose and usage:

  - **Agent Runtime** : This is the environment where the agent's core logic, decision-making, and orchestration run. It is a trusted environment that executes your code and manages the agent's lifecycle.
  - **Sandbox** : This is an auxiliary environment spawned *by* the agent or the platform to execute specific, potentially unsafe tasks. Sandboxes are typically short-lived or session-based, maintaining state only for the duration of a task or a user session. For example, if an agent needs to calculate a complex formula by generating and running a Python script, it should run that script in a sandbox, not in its own runtime.

## Features

Sandboxes offer several features such as predefined sandboxes, custom containers, and snapshots:

  - **[Code execution](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/code-execution-overview)** : Allows the agent to generate and run code in a secure environment. This is useful for complex mathematical calculations, data analysis, and other tasks that require computation.
  - **[Computer use](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/computer-use)** : Enables the agent to interact with a web browser to perform tasks such as filling out forms, searching the web, or navigating complex UI workflows.
  - **[Custom containers](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/custom-containers)** : You can "Bring Your Own Container" to customize the execution environment with specific libraries, tools, or configurations.
  - **[Snapshots](https://docs.cloud.google.com/gemini-enterprise-agent-platform/scale/sandbox/snapshots)** : You can save the state of a sandbox and restore it later, enabling lifecycle management, such as restoring a checkpoint or known good state.
