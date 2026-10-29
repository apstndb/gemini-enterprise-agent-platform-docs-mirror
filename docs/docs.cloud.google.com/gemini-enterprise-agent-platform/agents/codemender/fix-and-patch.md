---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/fix-and-patch
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/fix-and-patch
title: Fix code vulnerabilities and manage diffs
description: Learn how to generate, test, auto-apply, and stage automated code patches using CodeMender.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

CodeMender can automatically produce, validate, and apply source code patches for verified vulnerabilities, testing them in your local sandbox to prevent regressions.

## Generate vulnerability fixes

Use `cm fix` to generate a validated security patch for a verified finding:

```
cm fix FINDING_ID
```

When you run `cm fix` , CodeMender performs the following validation steps:

1.  **Generates a patch candidate** using the cloud-hosted reasoning engine.
2.  **Applies the patch** to a copy of the source code inside your local sandbox.
3.  **Compiles and tests** the codebase by running your configured `build.command` to ensure the project builds and unit tests pass.
4.  **Re-runs the verified PoC exploit** to confirm that the vulnerability is no longer exploitable.

By default, CodeMender prompts you to confirm each file modification before writing it to disk in your workspace. Once all checks pass, CodeMender applies the verified patch to your workspace. You can then stage the changes.

### Fix flags

- **Provide fix context ( `-c` / `--context` )** : Provide architectural constraints or coding guidelines:

  ```
  cm fix FINDING_ID -c "Use the safe parameterized database helper in src/db/query.go"
  ```

- **Auto-approve prompts ( `-y` / `--yes` )** : Auto-approve all file writes and command confirmation prompts during the fix process:

  ```
  cm fix FINDING_ID -y
  ```

  **Note:** You can also disable interactive confirmation prompts in your `config.yaml` by setting `tools.confirm_writes: false` and `tools.confirm_commands: false` .

- **Control sandboxing ( `--sandbox` )** : Explicitly enable or disable the OS-level sandbox for this run (for example, `--sandbox=false` to disable):

  ```
  cm fix FINDING_ID --sandbox=false
  ```

- **Bypass path boundaries ( `--allow-all-paths` )** : Disable the workspace path boundary check for this run so agent tools can access paths outside the project root and configured `project_paths` (combine with `--sandbox=false` to access host paths that aren't mounted inside the sandbox):

  ```
  cm fix FINDING_ID --allow-all-paths
  ```

- **Bypass command policy ( `--allow-all-commands` )** : Disable `command_policy.yaml` blocklist enforcement for this run:

  ```
  cm fix FINDING_ID --allow-all-commands
  ```

- **Bypass cache ( `--no-cache` )** : Force CodeMender to generate a fresh patch:

  ```
  cm fix FINDING_ID --no-cache
  ```

## Inspect and manage local VCS diffs

CodeMender includes built-in VCS commands to help you inspect, stage, and manage code changes that patches introduce before you commit them:

- **View repository status** : Check which files CodeMender modified or created in your local workspace.

  ```
  cm vcs status
  ```

- **Inspect diffs** : Review line-by-line unified diffs of all uncommitted code modifications the agent generated.

  ```
  cm vcs diff
  ```

- **Stage changes** : Add verified patch modifications to your local staging environment so you can test and commit them.

  ```
  cm vcs stage
  ```

- **Revert session modifications** : Discard all local file modifications CodeMender generated during the current session and restore your repository to its baseline state.

  ```
  cm vcs reset
  ```
