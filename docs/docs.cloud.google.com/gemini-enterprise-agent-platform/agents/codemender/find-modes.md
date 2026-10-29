---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/find-modes
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/find-modes
title: CodeMender find modes
description: Learn how to choose between a deep scan (default), a diff scan (--diff), and a quick scan (--quick) when scanning codebases with CodeMender.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) , and the [Additional Terms for Generative AI Preview Products](https://cloud.google.com/trustedtester/aitos) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .
>
> Pre-GA products are in various stages of internal testing and review. As such, customers should closely supervise the use of CodeMender, and not use CodeMender in situations where serious errors cannot be corrected. This product is made available to Customers solely for limited testing and evaluation, and may not be used for commercial or production purposes.
>
> You may only use CodeMender to analyze (i) source code that you own or are authorized to use or (ii) open source code distributed under an OSI-approved license. You must use this offering solely for legitimate security defense purposes (and not for unauthorized testing, exploitation, or cyberattacks) in compliance with the [Google Cloud Acceptable Use Policy](https://cloud.google.com/terms/aup?e=48754805) and the [Generative AI Prohibited Use Policy](https://policies.google.com/terms/generative-ai/use-policy) . When using CodeMender built with a Gemini Cyber or Gemini Frontier Cyber model, your access to and use of those models is also governed by Section 31 of the [Service Specific Terms](https://cloud.google.com/terms/service-terms#1) .
>
> When disabling human confirmation of write and tool execution actions (as described in the [configuration file parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#configuration-file) ), Customer is responsible for such modification under Section 20(j) ("Modifying, Disregarding, or Disabling Safety Filters") of the Service Specific Terms. The customer agrees not to automatically bypass or circumvent other responses requiring human confirmation.

CodeMender provides three distinct scanning modes through the `cm find` command. Each mode is designed for a specific stage of the software development lifecycle, balancing speed, scope, and depth.

## Compare find modes

The following table compares the three `cm find` scanning modes:

| Mode                | Command                                   | Target scope                                                      | Typical runtime  | Best for                                                                                 |
|---------------------|-------------------------------------------|-------------------------------------------------------------------|------------------|------------------------------------------------------------------------------------------|
| Deep scan (default) | `cm find `` PATH`                         | Specified directory or repository                                 | Longer runtime   | Comprehensive security audits, release readiness, compliance certifications (SOC 2, ISO) |
| Diff scan           | `cm find `` PATH `` --diff[= `` REF `` ]` | Modified files plus dependent files (such as callers and callees) | Fast runtime     | Pull request CI/CD pipelines (GitHub Actions, Cloud Build), pre-commit hooks             |
| Quick scan          | `cm find `` PATH `` --quick`              | Specified directory                                               | Moderate runtime | Local developer discovery, quick checks, exploratory reviews                             |

## Deep scan (default)

A deep scan is the default mode when you run `cm find` without providing additional scanning flags (the `--deep` flag is also supported for backward compatibility). It is an exhaustive scanning mode designed for comprehensive security audits. It audits source files across the target directory or repository concurrently using parallel workers (configured with `--deep-workers` , which defaults to `8` and supports a range of `1` to `16` ). As it discovers candidate findings, it validates and corroborates them against surrounding code context to filter out false positives before reporting results.

The following examples demonstrate how to run a deep scan across a repository:

```
# Run an exhaustive deep scan across the repository (default mode)
cm find .

# Tune concurrency and use the cyber-specialized security model
cm find . --deep-workers=8 --model=gemini-3.8-flash-cyber
```

### Strengths

A deep scan runs with zero configuration and delivers high recall and comprehensive vulnerability discovery across large enterprise codebases. It outperforms single-session scans and uses automated verification to maintain high precision. It is also platform-independent and works across all languages supported by Gemini without requiring language-specific compilers, build setups, or grammar files. Finally, it optimizes resource usage by focusing analysis on production code and minimizing compute and token consumption on non-production files.

### Trade-offs and limitations

Don't use a deep scan as a synchronous check that blocks pull requests. Deep scans perform a thorough, file-by-file analysis. As a result they require a longer runtime and higher token spend than quick or diff scans.

### When to use

Use a deep scan in the following scenarios:

- Run scheduled security audits on a nightly or weekly schedule across all production repositories.
- Perform a full pre-release security audit before major version releases or production deployments.
- Generate audit evidence for SOC 2, ISO 27001, FedRAMP, or PCI-DSS compliance and certification reviews.
- Establish an initial security baseline when onboarding a new codebase to CodeMender.

## Diff scan

A diff scan performs Git diff analysis for pull request workflows and CI/CD pipelines by inspecting modified and added files, focusing on the exact line ranges (diff hunks) that changed. In addition to inspecting changed lines, it performs impact analysis to discover untouched files in the repository that call, import, or depend on the modified functions and symbols. This helps ensure that changes altering contracts or function signatures in one file don't introduce vulnerabilities in dependent files.

During the scan, CodeMender automatically isolates pre-existing vulnerabilities in untouched code so that legacy issues don't cause the scan to fail or block the pull request. It then evaluates findings against your `--fail-on` policy and outputs results in table, JSON, or SARIF v2.1.0 format.

The following examples demonstrate how to run a diff scan against working copy changes, staged changes, or a target branch:

```
# Scan working copy changes versus HEAD
cm find . --diff

# Scan staged changes only (pre-commit)
cm find . --diff --staged

# Scan a pull request branch against the main branch in CI/CD
cm find . --diff=origin/main --format=sarif --output=results.sarif \
    --fail-on=CRITICAL,HIGH
```

For end-to-end pipeline configurations, see [Integrate with CI/CD](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/integrate-with-cicd) .

### Strengths

A diff scan is fast and deterministic, typically finishing in under 2 minutes to keep CI/CD pipeline runtimes short. Unlike diff scanners that only inspect changed lines, `--diff` inspects caller and callee relationships to catch cross-file security regressions and contract breaches. Because it suppresses findings in untouched code, the scan only blocks pull requests on issues introduced or affected by the changes, avoiding noisy reports and unnecessary build failures. A diff scan also emits SARIF v2.1.0 for direct integration into GitHub Code Scanning annotations and Cloud Build dashboards.

### Trade-offs and limitations

A diff scan only analyzes code within the affected area of the pull request and doesn't find pre-existing vulnerabilities in untouched parts of the repository. It also requires a Git repository with access to the target base reference.

### When to use

Use a diff scan in the following scenarios:

- Run automated checks on every pull request in CI/CD pipelines such as GitHub Actions, Cloud Build, GitLab CI, or Jenkins.
- Verify that local changes are clean in pre-commit or pre-push hooks before pushing code to the remote repository.
- Validate that merges between release branches don't introduce regressions.

## Quick scan

A quick scan ( `cm find --quick` ) runs a single-session autonomous scan of the specified target directory instead of the default concurrent per-file deep scan. During the scan, CodeMender discovers source files, prioritizes them based on vulnerability patterns, performs an initial security analysis, and reports potential vulnerabilities grouped by severity and type.

The following examples demonstrate how to run a quick scan on a target directory:

```
# Run a single-session quick scan on a directory using the default model
cm find ./src --quick

# Run a quick scan with a specific Gemini model
cm find ./src --quick --model gemini-3.8-flash
```

### Strengths

A quick scan balances speed and coverage with a moderate runtime and uses fewer tokens and less compute than a full deep scan, making it cost-effective for fast exploratory checks during everyday development.

### Trade-offs and limitations

A quick scan has lower recall on large codebases and might not explore every file in large, multi-package enterprise repositories because it operates within a single session context. It also focuses primarily on local patterns within individual files, which limits cross-package analysis and might miss vulnerabilities spanning distant packages.

### When to use

Use a quick scan in the following scenarios:

- Run a fast scan on your local machine to get quick feedback during local development.
- Inspect a newly cloned repository or a small project for a rapid initial assessment of its security posture.
- Inspect a specific subdirectory or module when doing a quick exploratory check.

## Choose a find mode

Use the following reference table to select the right scanning mode for your workflow:

| Workflow or environment     | Use case and goal                                         | Recommended mode | Example command                                        |
|-----------------------------|-----------------------------------------------------------|------------------|--------------------------------------------------------|
| Local terminal              | Quick discovery or confidence check on a specific module  | Quick scan       | `cm find ./src --quick`                                |
| Local terminal              | Pre-commit check on staged changes before pushing         | Diff scan        | `cm find . --diff --staged`                            |
| CI/CD pipeline              | Automated pull request gating on changed code and callers | Diff scan        | `cm find . --diff=origin/main --fail-on=CRITICAL,HIGH` |
| Scheduled pipeline or audit | Nightly audits, pre-release gates, SOC 2 compliance       | Deep scan        | `cm find . --deep-workers=8`                           |

## Command flag reference by mode

The following tables describe the command-line flags supported by each scanning mode.

### Common flags (all modes)

The following flags apply to all `cm find` scanning modes:

| Flag                    | Default            | Description                                                                                                                                                                                                                                                       |
|-------------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `-c, --context `` TEXT` | `""`               | Additional context to guide the scan agent, such as architecture notes.                                                                                                                                                                                           |
| `--model `` MODEL_NAME` | `gemini-3.8-flash` | Gemini model to use ( `gemini-3.8-flash` , `gemini-3.8-flash-cyber` ).                                                                                                                                                                                            |
| `-y, --yes`             | `false`            | Skip interactive confirmation prompts and the automatic update check. When the OS-level sandbox is enabled with default network isolation ( `permissive-closed` ), `cm find` mounts the workspace read-only and skips command confirmation prompts automatically. |
| `--sandbox`             | `true`             | Run commands inside the OS-level sandbox (for example, `--sandbox=false` to disable). In `cm find` , the sandbox mounts the workspace read-only.                                                                                                                  |
| `--allow-all-paths`     | `false`            | Disable the workspace path boundary check (combine with `--sandbox=false` to access host paths that aren't mounted inside the sandbox).                                                                                                                           |
| `--allow-all-commands`  | `false`            | Disable `command_policy.yaml` blocklist enforcement for this run.                                                                                                                                                                                                 |
| `--include-hidden`      | `false`            | Include hidden directories and files (starting with `.` ) during file discovery.                                                                                                                                                                                  |

### Deep scan flags

The following flags configure default `cm find` (or `cm find --deep` ) scans:

| Flag                      | Default | Description                                                                                                                                                                                                  |
|---------------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--deep`                  | `true`  | Run an exhaustive file-by-file deep scan (default mode when no mode flag is passed). Can't be used with `--diff` or `--quick` .                                                                              |
| `--deep-workers `` COUNT` | `8`     | Number of concurrent workers for per-file deep scans (1 to 16).                                                                                                                                              |
| `--enable-bash`           | `false` | Enable shell command execution ( `run_command` ) in per-file `--deep` workers (or set `CMOC_FIND_ENABLE_BASH=true` ). Quick scans ( `--quick` ) and diff scans ( `--diff` ) enable `run_command` by default. |

### Diff scan flags

The following flags configure `cm find --diff` scans:

| Flag                            | Default         | Description                                                                                                                                                             |
|---------------------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--diff[= `` REF `` ]`          | Off             | Enable diff mode against the target reference, such as `origin/main` or `HEAD~1` . Without `REF` , compares against `HEAD` . Can't be used with `--deep` or `--quick` . |
| `--staged`                      | Off             | Scope diff to staged index only ( `git diff --cached` ). Requires `--diff` .                                                                                            |
| `--diff-depth `` DEPTH`         | `1`             | Traversal depth for impact analysis (1 to 3, default: 1-hop).                                                                                                           |
| `--diff-workers `` COUNT`       | `4`             | Number of concurrent workers for pull request audit jobs (1 to 16).                                                                                                     |
| `--diff-max-neighbors `` COUNT` | `10`            | Maximum number of dependent caller or callee files to inspect.                                                                                                          |
| `--fail-on `` SEVERITIES`       | `CRITICAL,HIGH` | Comma-separated severities causing `cm find` to exit with code 1.                                                                                                       |
| `--fail-on-truncation`          | Off             | Exit with code 1 if neighbor discovery exceeds the cap.                                                                                                                 |
| `--format `` FORMAT`            | `table`         | Output format: `table` , `json` , or `sarif` .                                                                                                                          |
| `--output `` FILE`              | Standard output | Write report to a file instead of standard output.                                                                                                                      |

### Quick scan flags

The following flag configures `cm find --quick` scans:

| Flag      | Default | Description                                                                                                                     |
|-----------|---------|---------------------------------------------------------------------------------------------------------------------------------|
| `--quick` | `false` | Run a single-session quick scan instead of the default concurrent per-file deep scan. Can't be used with `--deep` or `--diff` . |
