---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/manage-sessions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/manage-sessions
title: Manage sessions and export reports
description: Learn how to list, resume, and cancel CodeMender sessions, as well as export HTML and Markdown reports.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

CodeMender tracks every scan, verification, and remediation attempt as a stateful session backed by a local SQLite database ( `state.db` ). You can inspect active sessions, resume paused tasks, and export detailed findings reports.

## Session management

The CodeMender CLI maintains stateful execution sessions locally, allowing you to track active tasks, resume interrupted workflows, and export security reports.

### List active and past sessions

Run the following command to list all sessions, their statuses ( `RUNNING` , `WAITING_FOR_TOOL` , `COMPLETED` , `FAILED` , `CANCELLED` ), and target paths:

    cm session list

### Resume an interrupted session

If a session pauses due to a network interruption or step failure, resume it from the latest checkpoint stage:

    cm session resume SESSION_ID

### Cancel a running session

To terminate an active session and stop backend agent compute execution:

    cm session cancel SESSION_ID

## View reports and export patches

Display session findings, verification statuses, and patch details using `cm report` .

### Output formats

### Terminal table (default)

Summarized list of findings.

    cm report

### HTML report

Generate a formatted HTML report. Use `--open` (or `-o` ) to automatically launch it in your default browser.

    cm report --format html --open

### Markdown

Generate a GitHub-flavored Markdown report.

    cm report --format md

### JSON

Export all session findings details as raw JSON.

    cm report --format json

### SARIF

Export findings in standard SARIF format (v2.1.0) for integration with other security tools.

    cm report --format sarif

### Filtering and sorting flags

  - **Display proposed code patches ( `--patches` )** : Include full unified diffs of generated fixes in the report. `bash cm report --patches`

  - **Filter by severity ( `--severity` )** : View findings matching a level ( `CRITICAL` , `HIGH` , `MEDIUM` , `LOW` ). `bash cm report --severity HIGH`

  - **Filter by status ( `--status` )** : View findings matching a state ( `OPEN` , `FIXED` , `DISMISSED` , `REOPENED` ). `bash cm report --status OPEN`

  - **Filter by session ( `--session` )** : View findings from a specific session ID prefix.
    
        cm report --session SESSION_ID_PREFIX

  - **Show agent artifacts ( `--artifacts` )** : Include paths to agent-generated run artifacts (like logs, exploit scripts). `bash cm report --artifacts`

  - **Sort findings ( `--sort` )** : Sort the results by `severity` (default) or `time` . `bash cm report --sort time`

  - **Filter by finding ID** : Pass a specific finding ID (or prefix) as a positional argument to view details for a single finding.
    
        cm report FINDING_ID_PREFIX

### Vulnerability finding states

CodeMender tracks findings across the following vulnerability states:

  - **`OPEN`**
      - **What it means:** The vulnerability has been successfully detected during a scan (or imported from a third-party tool) but has not yet been verified, patched, or marked as inactive.
      - **How it is handled:** This is the initial state of any newly discovered security flaw. Vulnerabilities in the `OPEN` state are actively queued for verification ( `cm verify` ) or patching ( `cm fix` ).
  - **`FIXED`**
      - **What it means:** CodeMender has generated a patch for the vulnerability, applied the diff to your local codebase, and successfully compiled and executed verify tests to prove the exploit no longer succeeds.
      - **How it is handled:** Once a patch is confirmed to resolve the issue without breaking existing code logic, CodeMender transitions the finding to `FIXED` . It will remain in this state unless a future scan detects a regression.
  - **`DISMISSED`**
      - **What it means:** The vulnerability is designated as inactive, either because it was identified as a false positive or already fixed, or the finding has insufficient confidence to confirm as exploitable (including against your project's threat model if one was provided during onboarding).
      - **How it is handled:** Marking an item as `DISMISSED` mutes future alerts and excludes the finding from your active CLI output with `cm report --status OPEN` . Re-running `cm verify` on a dismissed finding re-examines or restores dismissed items.
  - **`REOPENED`**
      - **What it means:** A vulnerability that was previously marked as `FIXED` or `DISMISSED` has been re-detected in a subsequent codebase scan.
      - **How it is handled:** This state indicates a regression (such as a bad git merge reverting the patch) or a failed mitigation strategy. It flags the issue for immediate re-evaluation and requires developers to review the patching process.

### Vulnerability severity levels

CodeMender categorizes findings into the following severity levels:

  - **`CRITICAL`**
      - **What it means:** The vulnerability poses an immediate, severe risk to your application or underlying infrastructure, potentially leading to full system compromise.
      - **Why it's categorized as Critical:** It meets high-consequence impact thresholds (like Remote Code Execution or root-level writes), is directly reachable from untrusted boundaries without prerequisites, and is backed by high-confidence taint-flow analysis or a validated Proof of Concept (PoC) executed inside CodeMender's sandbox.
  - **`HIGH`**
      - **What it means:** The vulnerability represents a severe security flaw that could lead to unauthorized system control, privilege escalation, or significant data exposure, but requires specific conditions to execute.
      - **Why it's categorized as High:** While the impact of exploitation is high (e.g., arbitrary database reads or administrative hijacking), the exploitability is slightly constrained. It might require an attacker to have standard user authentication, depend on a specific system configuration, or require a highly precise chain of actions.
  - **`MEDIUM`**
      - **What it means:** The vulnerability presents a moderate risk, typically exposing restricted data or allowing localized disruptions, but is low risk to the host system.
      - **Why it's categorized as Medium:** The exploit is heavily gated by reachability or complexity. It generally requires active user interaction (like clicking a malicious link), deep privileges, or complex conditions to bypass defensive layers, and its ultimate affected area is restricted.
  - **`LOW`**
      - **What it means:** The finding represents a minor security risk or a general lack of defense-in-depth hygiene that does not present an immediate threat on its own.
      - **Why it's categorized as Low:** It features extremely low exploitability or minimal impact. The finding is typically used by attackers for reconnaissance or configuration fingerprinting rather than direct compromise, and it cannot be used to execute arbitrary code or exfiltrate sensitive application data.

## Workspace maintenance

To reset local state tracking files and clean up temporary execution caches, run:

    cm clean
