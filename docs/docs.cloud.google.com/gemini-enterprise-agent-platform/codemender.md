---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender
title: CodeMender overview
description: Gemini Enterprise Agent Platform is a central console designed for platform and security administrators to build, scale, monitor, optimize, and govern the entire lifecycle of AI agents.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

> Pre-GA products are in various stages of internal testing and review. As such, customers should closely supervise the use of CodeMender, and not use CodeMender in situations where serious errors cannot be corrected. This product is made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.
> 
> When disabling human confirmation of write and tool execution actions (as described in the [configuration file parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#configuration-file) ), Customer is responsible for such modification under Section 20(j) (“Modifying, Disregarding, or Disabling Safety Filters”) of the Service Specific Terms. The customer agrees not to automatically bypass or circumvent other responses requiring human confirmation.

The launch of advanced AI models triggered widespread concern regarding code vulnerabilities. As attackers gain access to new capabilities for generating exploits, security teams are under immense time pressure to proactively find and fix vulnerabilities before attackers exploit them.

CodeMender is an AI code security agent that can find, verify, and fix deep vulnerabilities in your codebase. CodeMender wraps a fine-tuned harness around an LLM, using Google DeepMind-engineered prompts, skills, and orchestration logic to turn the model into an agentic system specialized in code security.

## How it works

> **Note:** CodeMender is currently available to a limited set of customers in Public Preview. Contact your sales team to get access.

CodeMender handles the scale and diversity of modern corporate environments, where code spans numerous languages and system types:

  - **Find vulnerabilities** by scanning your codebase using an LLM guided by the agent, leveraging specialized tools and prompt engineering to focus the model on security flaws. Alternatively, you can import a list of vulnerabilities from external security scanning tools.
  - **Verify vulnerabilities** by building the code and attempting to exploit found vulnerabilities to verify whether they are exploitable. This helps prioritize confirmed vulnerabilities and reduces the false positive rate.
  - **Fix vulnerabilities** by generating and testing a patch that is compatible with the language of your codebase.

During all three stages, you can provide context to CodeMender to ensure it accounts for the nuances of your application and threat model. This combination of an LLM with CodeMender's fine-tuned harness provides higher-quality results versus using an LLM alone to find and fix vulnerabilities.

## System architecture

From a user perspective, the CodeMender system consists of two components:

  - **Agent** : A hosted multi-agent system that runs the core business logic and reasoning.
  - **Client** : A client running on your machine, acting as both a CLI (to issue commands and view outputs) and a daemon (to execute commands on behalf of the agent, with optional isolation inside a local process-level sandbox to safely compile code, run tests, and verify vulnerabilities).

## Supported languages and frameworks

CodeMender supports top vulnerability types across all major programming languages: C/C++, Go, Java, Python, TypeScript / JavaScript, Rust, and Ruby. Additionally, it has broad support for standard libraries within these languages, as well as common enterprise frameworks (such as HTML/CSS, Django, Flask, React, Spring Boot, and Express).

Supported vulnerability types cover a wide spectrum of software security flaws across application logic, data handling, memory management, and authentication control flows.

## Supported models

CodeMender supports the following models:

#### Click to expand supported models

  - [Gemini 3.5 Flash](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-5-flash)
  - [Gemini 3.1 Pro](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/gemini/3-1-pro) preview

To specify a model when running CodeMender CLI commands, see [Specifying the model](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender#specifying-the-model) .

## Supported regions

CodeMender is globally available.

## Track token usage

CodeMender surfaces token consumption in two places: a live status line while a command runs, and a one-line summary when a command completes successfully. Counts cover input, output, and total tokens for the current session.

### Live status line

While `cm find` , `cm fix` , `cm verify` , or `cm session resume` is running, pass the `--compact` flag to display a rolling status line that updates as the agent works:

    cm find ./src/auth/ --compact

The status line reports cumulative session totals:

    Tokens: 40k in / 12k out / 60k total

Resumed sessions continue counting from where the prior run left off. The `total` count may include the model's internal reasoning tokens, so it can exceed `in + out` .

### Exit summary

When a command finishes successfully and at least one tool step was executed, CodeMender prints a one-line summary with elapsed time and token totals:

    ✅ Completed 14 tool steps in 3m 42s | Tokens: 40k in / 12k out / 60k total

### Billed token usage

To view cumulative billed token usage and cost trends across your Google Cloud project, see [View your billing reports and cost trends](https://docs.cloud.google.com/billing/docs/how-to/reports) in Cloud Billing.

## Get started with the CLI

Set up the CLI tool and initialize your workspace to start scanning.

> **Warning:** CodeMender executes commands and may modify files directly on your host system. By default, these commands run inside a local process-level sandbox. If you disable the sandbox (in `config.yaml` or using the `--sandbox=false` flag) or bypass it (using the `--unrestricted` flag), we highly recommend running the CLI in an isolated VM or container to protect your host system.

### Prerequisites

Before you initialize the CodeMender CLI, ensure your environment is prepared correctly:

  - **[Set up Google Cloud project](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#gcp-project-setup-iam-permissions) :** Set up your Google Cloud project with required APIs and IAM roles.
  - **[Download the CodeMender CLI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#download-cli) :** Download and install the CodeMender CLI binary for your operating system.
  - **[Configure Google Cloud credentials](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#configure-credentials) :** Configure Google Cloud Application Default Credentials (ADC) to authenticate the CLI.
  - **Provision your source code:** Clone or copy the source code of the project you want to scan into your workspace.
  - **[Configure Sandbox](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#sandbox-configuration) :** Define directory mounts, network access profiles, and security exceptions for the sandbox environment.

### Specifying the model

By default, CodeMender uses Gemini 3.5 Flash. To override the default model, pass the `--model` flag with the corresponding model identifier:

  - Gemini 3.5 Flash (default): `--model gemini-3.5-flash`
  - Gemini 3.1 Pro Preview: `--model gemini-3.1-pro-preview`

The following commands support the `--model` flag:

  - `cm find`
  - `cm verify`
  - `cm fix`

To specify a model when running any of these commands, use the following syntax:

    cm COMMAND TARGET --model MODEL_NAME

## Security and data privacy

The following sections outline CodeMender's security model, data retention policies, and access controls:

### What data does CodeMender send to the cloud?

When using CodeMender, the local CLI tool mediates access to your code, ensuring that you never upload your full source code repositories to Google's servers and the hosted agent does not independently clone them.

Instead, the CLI strictly localizes the data it sends to the Google-hosted agent, which consists of:

  - Targeted file contents or code snippets, vulnerability information, proposed patches, and command execution results.
  - Metadata, diagnostics, errors, and usage telemetry (such as tokens consumed and command duration).

**We never use your customer source code to train the underlying model weights.**

### What is the retention policy?

CodeMender uses a strict, short-term data retention policy:

  - **7-day maximum retention:** We retain session data, including code snippets and tracking states, for up to 7 days in Gemini Enterprise Agent Platform storage to allow users to seamlessly resume interrupted scans. After 7 days, the system automatically deletes it (see [Zero Data Retention](https://docs.cloud.google.com/gemini-enterprise-agent-platform/resources/zero-data-retention) ).
  - **Explicit deletion:** Customers do not have to wait 7 days; they can trigger an immediate cleanup of all session data by calling `DeleteInteraction` .
  - **Ephemeral findings:** We do not store vulnerability findings and patches in long-lived databases; they accumulate in-memory during the pipeline.

### Who can access the data?

CodeMender uses a "Zero-Data-Access" approach regarding human visibility:

  - **No human access:** No human groups or Google engineers have access to read customer data in the production environment.
  - **No operator visibility:** Even for production debugging and error tracking, Google operators are restricted and do not have visibility into customer source code context or transient session states.
  - **Strict isolation:** We logically isolate and access-control all data by organization and customer billing-project to protect tenant privacy within our shared infrastructure.
  - **VPC Service Controls (VPC-SC):** To further protect your environment, CodeMender's architecture fully supports VPC Service Controls (VPC-SC). This lets you define a secure security perimeter around your Google Cloud resources, helping to mitigate any data exfiltration risks while your localized data is sent to the cloud reasoning engine.

## What's next

For detailed instructions, see the following guides:

  - [Install and configure the CLI](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment)
  - [Scan and verify code vulnerabilities](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/scan-and-verify)
  - [Import third-party security findings](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/import-findings)
  - [Fix code vulnerabilities and manage diffs](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/fix-and-patch)
  - [Manage sessions and export reports](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/manage-sessions)
