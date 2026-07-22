---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/manage-sessions
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/manage-sessions
title: Manage sessions and export reports
description: Learn how to list, resume, and cancel CodeMender sessions, as well as export HTML and Markdown reports.
data_source: docs.cloud.google.com
---

> **Preview**
> 
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

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

## Workspace maintenance

To reset local state tracking files and clean up temporary execution caches, run:

    cm clean
