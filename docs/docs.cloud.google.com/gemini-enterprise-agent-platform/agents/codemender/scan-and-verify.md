---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/scan-and-verify
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/scan-and-verify
title: Scan and verify code vulnerabilities
description: Learn how to scan codebases for security flaws and run proof-of-concept exploits to verify vulnerability exploitability.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
>
> Pre-GA products are in various stages of internal testing and review. As such, customers should closely supervise the use of CodeMender, and not use CodeMender in situations where serious errors cannot be corrected. This product is made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.
>
> You may only use CodeMender to analyze (i) source code that you own or are authorized to use or (ii) open source code distributed under an OSI-approved license. You must use this offering solely for legitimate security defense purposes (and not for unauthorized testing, exploitation, or cyberattacks) in compliance with the [Google Cloud Acceptable Use Policy](https://cloud.google.com/terms/aup?e=48754805) and the [Generative AI Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) . When using CodeMender built with a Gemini Cyber model, your access to and use of that model are also governed by Section 31(a) of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) (Gemini Cyber).
>
> When disabling human confirmation of write and tool execution actions (as described in the [configuration file parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#configuration-file) ), Customer is responsible for such modification under Section 20(j) ("Modifying, Disregarding, or Disabling Safety Filters") of the Service Specific Terms. The customer agrees not to automatically bypass or circumvent other responses requiring human confirmation.

CodeMender lets you proactively scan your codebase for software weaknesses and execute proof-of-concept (PoC) exploits in your local sandbox to confirm exploitability and eliminate false positives.

## Scan for vulnerabilities

To run a rapid security scan across your codebase, run `cm find` . Scan targeted modules or batches of 10 to 50 files at a time for optimal performance.

Scan a specific subdirectory:

```
cm find ./src/auth/
```

Scan only the modified files in a subdirectory:

```
cm find --diff ./src/auth/
```

Scan a single file:

```
cm find ./src/auth/session_manager.py
```

Skip interactive approval prompts during the scan:

```
cm find ./src/auth/ -y
```

For more information about scanning pull requests with `--diff` or running deep multi-session scans with `--deep` , see [CodeMender find modes](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/find-modes) and [Integrate with CI/CD](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/integrate-with-cicd) .

## Verify vulnerabilities

> **Warning:** CodeMender executes commands and may modify files directly on your host system. By default, these commands run inside a local process-level sandbox. If you disable the sandbox (in `config.yaml` or using the `--sandbox=false` flag) or bypass it (using the `--unrestricted` flag), run the CLI in an isolated VM or container to protect your host system.

Once CodeMender identifies potential vulnerabilities, ask it to verify exploitability. During verification, CodeMender generates and executes a proof-of-concept (PoC) exploit (inside the default [sandbox](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#execution-sandboxing) ) to confirm whether the issue is genuinely exploitable.

Locate the `finding-id` from the output of `cm report` or `cm find` , then run:

```
cm verify FINDING_ID
```

### Verification flags

The following flags configure `cm verify` :

| Flag                          | Default | Description                                                                                                                                                                               |
|-------------------------------|---------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-c, --context `` TEXT`       | `""`    | Pass steering instructions or application domain context to guide the agent (for example, `cm verify `` FINDING_ID `` -c "Focus analysis on the multi-tenant session validation path"` ). |
| `--skip-exploit-verification` | `false` | Perform static verification only without running active PoC exploits.                                                                                                                     |
| `--sandbox`                   | `true`  | Explicitly enable or disable the sandbox for this run (for example, `--sandbox=false` to disable).                                                                                        |
| `--unrestricted`              | `false` | Temporarily bypass all sandbox protections for this run, disabling file system boundaries and OS-level container isolation.                                                               |
| `-y, --yes`                   | `false` | Skip interactive confirmation prompts ( `[y/N]` ) for tool actions and PoC exploit execution. Commands remain contained within the OS-level sandbox container ( `exebox` ).               |
