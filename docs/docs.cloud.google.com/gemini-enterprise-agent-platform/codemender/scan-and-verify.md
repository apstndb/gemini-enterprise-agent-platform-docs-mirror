---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/scan-and-verify
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/scan-and-verify
title: Scan and verify code vulnerabilities
description: Learn how to scan codebases for security flaws and run proof-of-concept exploits to verify vulnerability exploitability.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

CodeMender lets you proactively scan your codebase for software weaknesses and execute proof-of-concept (PoC) exploits in your local sandbox to confirm exploitability while eliminating false positives.

## Scan for vulnerabilities

To run a rapid security scan across your codebase, run `cm find` . We recommend scanning targeted modules or batches of 10 to 50 files at a time for optimal performance.

Scan a specific subdirectory:

    cm find ./src/auth/

Scan a single file:

    cm find ./src/auth/session_manager.py

Skip interactive approval prompts during the scan:

    cm find ./src/auth/ -y

## Verify vulnerabilities

> **Warning:** CodeMender may modify files or execute commands on your system. It is highly recommended to run the CLI in a safe sandbox environment or isolated VM.

Once potential vulnerabilities are identified, ask CodeMender to verify exploitability. During verification, CodeMender generates and executes a proof-of-concept (PoC) exploit in your sandbox to confirm whether the issue is genuinely exploitable.

Locate the `finding-id` from the output of `cm report` or `cm find` , then run:

    cm verify FINDING_ID

### Verification flags

  - **Provide custom guidance context ( `-c` / `--context` )** : Pass steering instructions or application domain context to guide the agent:
    
        cm verify FINDING_ID -c "Focus analysis on the multi-tenant session validation path"

  - **Skip PoC exploit execution ( `--skip-exploit-verification` )** : Perform static verification only without running active exploits:
    
        cm verify FINDING_ID --skip-exploit-verification

  - **Auto-approve prompts ( `-y` )** : Skip confirmation prompts:
    
        cm verify FINDING_ID -y
