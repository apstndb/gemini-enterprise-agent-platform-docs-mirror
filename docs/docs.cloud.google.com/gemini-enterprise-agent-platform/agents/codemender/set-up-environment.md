---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment
title: Install and configure the CLI
description: Learn how to download the CodeMender CLI, configure {{dynamic_data.site_values.cloud_name}} credentials and project, and initialize your workspace.
data_source: docs.cloud.google.com
---

> **Preview**
>
> This product or feature is subject to the "Pre-GA Offerings Terms" in the General Service Terms section of the [Service Specific Terms](https://docs.cloud.google.com/terms/service-terms#1) . Pre-GA products and features are available "as is" and might have limited support. For more information, see the [launch stage descriptions](https://cloud.google.com/products/#product-launch-stages) .

CodeMender is an autonomous AI code security agent that scans, verifies, and patches deep cybersecurity vulnerabilities in your codebase. Before running CodeMender, download the CLI and initialize workspace options.

## Architecture and security model

CodeMender uses a **local-first execution model** :

- **Hosted reasoning engine** : Agentic reasoning, threat modeling, and orchestration logic run securely in Google Cloud on Gemini Enterprise Agent Platform.
- **Local execution CLI** : Source code never leaves your workstation or CI/CD container in bulk. Local `cm` CLI tool executes file reads, local build checks, and proof-of-concept (PoC) exploit verifications in your local sandbox, sending only surgical code snippets and tool execution results to the cloud backend over the Interactions API on Gemini Enterprise Agent Platform.

## Environment setup

To begin using CodeMender, set up your Google Cloud project, download and install the CLI, configure your credentials and target project, and initialize your workspace.

### Project setup and IAM permissions

Before downloading the CLI and configuring credentials, ensure that the target Google Cloud project is set up correctly with the required APIs and permissions.

#### Required APIs

Ensure the following Google Cloud APIs are enabled in your project:

1.  **Agent Platform API** ( `aiplatform.googleapis.com` ) — Powers the streaming and management of active sessions.
2.  **Cloud Resource Manager API** ( `cloudresourcemanager.googleapis.com` ) — Validates user authentication states and project metadata.

#### Recommended predefined IAM role

To run the CLI commands, users should be assigned the following IAM role:

- **Agent Platform User** ( `roles/aiplatform.user` ) — Allows users to create, stream, and manage active sessions.

### Download and install CodeMender CLI

The CodeMender CLI binaries are hosted in Artifact Registry. Choose the tab for your operating system to download and install the CLI.

> **Note:** CodeMender is currently available to a limited set of customers in Public Preview. Contact your sales team to get access.

### Linux x86_64

To download and install CodeMender CLI for Linux (x86_64):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command:

      ```
      gcloud artifacts generic download \
        --project=cmoc-prod \
        --location=us \
        --repository=codemender-cli-production \
        --package=cm \
        --version=stable \
        --name=cm-linux-amd64.zip \
        --destination=./
      ```

    - **curl:** Run the following command:

      ```
      curl -L -o cm-linux-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-amd64.zip:download?alt=media"
      ```

2.  Install the CLI:

    ```
    unzip cm-linux-amd64.zip
    chmod +x cm
    sudo mv cm /usr/local/bin/cm
    ```

### Linux ARM64

To download and install CodeMender CLI for Linux (ARM64):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command:

      ```
      gcloud artifacts generic download \
        --project=cmoc-prod \
        --location=us \
        --repository=codemender-cli-production \
        --package=cm \
        --version=stable \
        --name=cm-linux-arm64.zip \
        --destination=./
      ```

    - **curl:** Run the following command:

      ```
      curl -L -o cm-linux-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-arm64.zip:download?alt=media"
      ```

2.  Install the CLI:

    ```
    unzip cm-linux-arm64.zip
    chmod +x cm
    sudo mv cm /usr/local/bin/cm
    ```

### macOS Intel

To download and install CodeMender CLI for macOS (Intel):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command:

      ```
      gcloud artifacts generic download \
        --project=cmoc-prod \
        --location=us \
        --repository=codemender-cli-production \
        --package=cm \
        --version=stable \
        --name=cm-darwin-amd64.zip \
        --destination=./
      ```

    - **curl:** Run the following command:

      ```
      curl -L -o cm-darwin-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-amd64.zip:download?alt=media"
      ```

2.  Install the CLI:

    ```
    unzip cm-darwin-amd64.zip
    chmod +x cm
    mv cm /usr/local/bin/cm
    ```

### macOS Apple silicon

To download and install CodeMender CLI for macOS (Apple silicon):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command:

      ```
      gcloud artifacts generic download \
        --project=cmoc-prod \
        --location=us \
        --repository=codemender-cli-production \
        --package=cm \
        --version=stable \
        --name=cm-darwin-arm64.zip \
        --destination=./
      ```

    - **curl:** Run the following command:

      ```
      curl -L -o cm-darwin-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-arm64.zip:download?alt=media"
      ```

2.  Install the CLI:

    ```
    unzip cm-darwin-arm64.zip
    chmod +x cm
    mv cm /usr/local/bin/cm
    ```

### Windows x86_64

To download and install CodeMender CLI for Windows (x86_64):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command in PowerShell:

      ```
      gcloud artifacts generic download `
        --project=cmoc-prod `
        --location=us `
        --repository=codemender-cli-production `
        --package=cm `
        --version=stable `
        --name=cm-windows-amd64.zip `
        --destination=./
      ```

    - **PowerShell:** Run the following command:

      ```
      Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-amd64.zip:download?alt=media" -OutFile cm-windows-amd64.zip
      ```

2.  Install the CLI:

    ```
    Expand-Archive -Path cm-windows-amd64.zip -DestinationPath ./
    # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)
    ```

### Windows ARM64

To download and install CodeMender CLI for Windows (ARM64):

1.  Download the package using one of the following methods:
    - **gcloud CLI:** Run the following command in PowerShell:

      ```
      gcloud artifacts generic download `
        --project=cmoc-prod `
        --location=us `
        --repository=codemender-cli-production `
        --package=cm `
        --version=stable `
        --name=cm-windows-arm64.zip `
        --destination=./
      ```

    - **PowerShell:** Run the following command:

      ```
      Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-arm64.zip:download?alt=media" -OutFile cm-windows-arm64.zip
      ```

2.  Install the CLI:

    ```
    Expand-Archive -Path cm-windows-arm64.zip -DestinationPath ./
    # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)
    ```

### Configure Google Cloud credentials and project

Because the CodeMender CLI interacts with the cloud-hosted reasoning engine over the Interactions API, you must configure Google Cloud Application Default Credentials (ADC) and specify your target project in your environment.

1.  To authenticate, run the following command and follow the login prompts:

    ```
    gcloud auth application-default login
    ```

2.  Set the `GOOGLE_CLOUD_PROJECT` environment variable to your Google Cloud project ID:

    ```
    export GOOGLE_CLOUD_PROJECT="PROJECT_ID"
    ```

    Alternatively, configure your active gcloud CLI CLI project:

    ```
    gcloud config set project PROJECT_ID
    ```

    Replace `PROJECT_ID` with your Google Cloud project ID.

## Initialize the workspace

After configuring your credentials and target project, your next step is to initialize CodeMender in your local environment. Initializing CodeMender prepares your local workspace by creating state-tracking files and establishing connection settings to the cloud-hosted reasoning engine.

Run `cm init` from the root directory of your codebase to create local state tracking files and establish baseline configurations:

```
cm init
```

Use the `--verify` flag to test connectivity to the cloud-hosted reasoning engine and verify workspace settings:

```
cm init --verify
```

> **Note:** If you encounter the message `Resource setup has just started. Please try again shortly.` , initial resource provisioning is underway and typically completes within a few minutes.

### Check service connectivity and permissions

To verify your credentials, configuration, network reachability, and IAM permissions without starting a scan or modifying your workspace, run `cm health` :

```
cm health
```

The `cm health` command runs four sequential checks and stops at the first failing layer. You can run `cm health` from any directory, even before you run `cm init` . It doesn't write to disk or consume model quota.

For automated CI/CD preflight checks or scheduled synthetic monitoring, use `--strict` to fail when project-level IAM checks are skipped, and `--json` to output a machine-readable JSON report:

```
cm health --strict --json
```

The following table describes the `cm health` exit codes:

| Exit code | Layer           | Description                                                                                                                                            |
|-----------|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| `0`       | —               | All health checks passed.                                                                                                                              |
| `10`      | `credentials`   | The CLI couldn't acquire a valid OAuth or Application Default Credentials token, or the server rejected the token ( `401 Unauthorized` ).              |
| `20`      | `config`        | The local `config.yaml` file, the `--team-id` flag, or the `CM_TEAM_ID` environment variable is invalid.                                               |
| `30`      | `reachability`  | The CLI couldn't reach the Agent Platform API endpoint (for example, due to DNS, TLS, proxy, or VPC Service Controls restrictions).                    |
| `40`      | `authorization` | The server was reached, but the caller or project isn't authorized to run CodeMender scans (for example, missing `roles/aiplatform.user` permissions). |
| `50`      | —               | The health check exceeded the `--timeout` duration (default `30s` ).                                                                                   |

The following flags are supported by `cm health` :

| Flag        | Default | Description                                                                                                                                                                                                                  |
|-------------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `--json`    | `false` | Outputs a single JSON object to standard output, including `status` , `exit_code` , `backend` , `endpoint` , `location` , `project_id` , `agent_id` , `duration_ms` , `layers` , and (when present) `warnings` and `error` . |
| `--strict`  | `false` | Treats health check warnings (such as unverified or skipped project-level IAM permission checks) as exit code `40` failures.                                                                                                 |
| `--timeout` | `30s`   | Sets the overall timeout for the health check probe.                                                                                                                                                                         |

## Configuration parameters ( `config.yaml` )

The primary goal of `config.yaml` is to **align CodeMender's agent behaviors with your local system's security, environment constraints, and performance needs** .

Since the hosted AI agent executes local commands (like building code, running tests, or editing files) using your local daemon client, this configuration file acts as the boundary defining what the agent is and isn't allowed to do.

### Usage

- **Location:** By default, the CLI reads this file from `~/.codemender/config.yaml` . You can override the workspace and configuration directory by setting the `CM_HOME` environment variable (for example, `CM_HOME=/path/to/custom/dir` , which reads `/path/to/custom/dir/config.yaml` ).
- **Execution:** When you run commands such as `cm find` , `cm verify` , or `cm fix` , the local client reads this file to set up safety parameters, apply system bypasses, and specify which files or directories to ignore.

### Core default settings

Here is what the core default parameters mean:

- **`tools.confirm_commands: true`**

  - **What it means:** By default, CodeMender prompts you for a `[Y/n]` confirmation in the terminal before executing shell commands ( `run_command` ). When `cm find` runs with the OS-level sandbox enabled ( `sandbox.enabled: true` ) and default network isolation ( `permissive-closed` ), the workspace is mounted read-only and command confirmation prompts are skipped automatically.
  - **Why this is the default:** CodeMender may run build commands, test suites, or exploit scripts during verification and patching. Requiring confirmation when the workspace is writable or unsandboxed helps prevent unintended command execution in your local environment.
  - **Bypass:** Pass `-y` (or `--yes` ) for a single run, or set `tools.confirm_commands: false` in `config.yaml` for non-interactive CI/CD pipelines.

- **`tools.confirm_writes: true`**

  - **What it means:** Prompts you for a `[Y/n]` confirmation in the terminal before the CodeMender agent writes or modifies files on disk ( `write_to_file` and `search_and_replace` ).
  - **Why this is the default:** Requiring manual confirmation prevents the agent from making speculative or unintended modifications to your source files during `cm fix` or `cm verify` . Only set this to `false` (or pass `-y` / `--yes` ) when running in isolated, disposable environments or automated CI/CD pipelines.

- **`execution.interactive_mode: true`**

  - **What it means:** Enables interactive terminal prompts during tool execution. Set this to `false` (or pass `-y` / `--yes` ) in headless CI/CD environments where no terminal is attached.

- **`scan.extensions.include: [".py", ".java", ".go", ".js", ".jsx", ".mjs", ".cjs", ".ts", ".tsx", ".c", ".cc", ".cpp", ".cxx", ".h", ".hh", ".hpp", ".hxx", ".inl", ".ipp", ".cs", ".rs", ".kt", ".kts", ".rb", ".php", ".sol", ".tf", ".hcl"]`**

  - **What it means:** Defines the explicit list of file extensions that you authorize CodeMender to ingest and analyze when scanning your workspace. CodeMender automatically skips any file in your repository with an extension not specified in this list.
  - **Why this is the default:** This list defaults to major programming languages to maximize scanning efficiency and prevent the agent from wasting time and tokens on irrelevant text files, build artifacts, or binary files. However, because modern applications often embed vulnerabilities in deployment configs or automation tools, you can manually expand this default list in `config.yaml` to include configuration files, script formats, and IaC files (for example, shell scripts, XML, YAML, properties, and JSON files) so CodeMender doesn't silently ignore them.

- **`scan.exclude_dirs: ["node_modules", "vendor", "dist", "/target", "/obj", "/build", ".gradle"]`**

  - **What it means:** CodeMender skips these directories during workspace scanning and code analysis. Entries with a leading `/` (such as `/target` , `/obj` , and `/build` ) match only at the scan root so nested source packages with those names aren't skipped.
  - **Why this is the default:** Large dependency or build folders trigger a massive latency and token penalty. Keeping these excluded by default ensures high performance and rapid response times. You can customize this list in `config.yaml` to include or exclude specific directories according to your project structure.

- **`project_paths: []`**

  - **What it means:** A list of directory paths that CodeMender can access (read/write) during tool execution.
  - **Why this is the default:** By default, it is empty, which restricts the agent to the enclosing project root (or scan target directory). If your build or test process requires accessing files outside the project root, add those paths here or pass `--allow-all-paths` for a single run. Writes to `.git` , `.hg` , and `.codemender` are always blocked.
  - **Artifacts directory:** The agent can also write to a per-session artifacts directory ( `~/.codemender/artifacts/<session_id>/` , or the equivalent under `$CM_HOME` ).
  - **Temporary files:** When the sandbox is enabled, the host `/tmp` directory is always blocked, even if you add `/tmp` to `project_paths` . Tools that respect `TMPDIR` use a temporary directory inside the artifacts directory instead.

- **`sandbox`** :

  - **What it means:** Configuration block for the process-level sandbox environment.
  - **Sub-parameters:**
    - **`enabled: true`** : (Boolean) Enables or disables the sandbox. If you set this to `true` (default), the agent runs tools inside the local sandbox. If you set it to `false` (or pass `--sandbox=false` ), the agent runs tools directly on the host system without OS-level isolation.
    - **`mounts`** : (Object)
      - **`target_dir: "."`** : (String) The directory to mount as the active workspace inside the sandbox. The CLI resolves relative paths against the workspace root.
    - **`network`** : (Object)
      - **`profile: "permissive-closed"`** : (String) Outbound network access profile inside the sandbox. Granular allow-listing of specific domains or URL patterns is not yet supported. Supported profiles:
        - `permissive-closed` (Default): Complete network isolation; the sandbox blocks all outbound connections.
        - `permissive-open` : Allows full outbound network access.

- **`security`** :

  - **What it means:** Configuration block for security policies.
  - **Sub-parameters:**
    - **`protected_files: []`** : (List of Strings) Additional files or directories on the host system that you want to mount **read-only** inside the sandbox to protect them from modification. Supports path expansion ( `~` ) and wildcards ( `*` ). Even when `protected_files` is empty, the sandbox always protects `.git/hooks` , `.git/config` , `.hg/hgrc` , and `.codemender` as read-only and excludes common credential directories ( `~/.ssh` , `~/.gnupg` , `~/.aws` , `~/.config/gcloud` , `~/.config/gh` , `~/.kube` , `~/.docker` ).

- **`model: "gemini-3.8-flash"`**

  - **What it means:** The default intelligence engine powering the backend reasoning loops.
  - **Why this is the default:** `gemini-3.8-flash` offers the optimal balance of speed, cost, and analytical reasoning required to suggest patches. (Users can override this to `gemini-4-argon` (Gemini 4 Argon) for deeper, more complex reasoning when needed).

- **`vcs: { type: "git" }`**

  - **What it means:** Defines the type of version control system your project uses through the `vcs` key. If you leave this unconfigured, the tool attempts to automatically identify Git or Mercurial repositories. If you set `vcs` to `none` , the CLI outputs a warning but continues execution without VCS functionality. CodeMender relies on this setting to manage speculative security fixes, track codebase modifications, and integrate with your local repository.
  - **Why this is the default:** CodeMender supports Git, Mercurial, or custom VCS configurations. Git is the default as it is the industry standard for version control tracking, ensuring seamless diff integration and rollback safety.

- **`build: { command: "make build && make test" }`**

  - **What it means:** Defines the exact shell command that CodeMender executes to compile and build your project, as well as run your unit and regression tests.
  - **Why this is the default:** Setting a build and test command is critical for the verification workflow. It allows CodeMender to compile your project and run your existing test suite in the isolated sandbox environment to prove that the generated security patch successfully mitigates the vulnerability without breaking existing application logic.

### Confirmation prompts

CodeMender asks for confirmation before it runs a shell command ( `tools.confirm_commands` ) and before it writes a file ( `tools.confirm_writes` ). The two settings are independent, and both default to `true` . The following settings turn off these prompts, in order of precedence:

1.  **`-y` or `--yes`** : Approves all command and file-write prompts for one run, whatever `config.yaml` says.
2.  **`execution.interactive_mode: false`** in `config.yaml` : Turns off both command and file-write prompts for every run.
3.  **`tools.confirm_commands: false`** or **`tools.confirm_writes: false`** in `config.yaml` : Turns off command prompts or file-write prompts for every run, independently of each other.

If none of these settings applies and no one can answer the prompt, for example in a CI/CD job without a terminal, CodeMender doesn't run the command or write the file.

Separately from these prompts, the CLI warns you that the agent can modify files and run commands on your system, and asks you to acknowledge the warning. `-y` doesn't skip this warning. To skip it, pass `--bypass-warning` . In a non-interactive environment without `--bypass-warning` , `cm` fails with `warning not acknowledged` . `cm find` skips the warning when the sandbox is enabled with the default `permissive-closed` network profile.

### Command policy ( `command_policy.yaml` )

In addition to the OS-level sandbox, you can define a command denylist in `~/.codemender/command_policy.yaml` (global) and `<project>/.codemender/command_policy.yaml` (project-specific). When both files are present, CodeMender merges their rules.

On first run, CodeMender creates a commented-out template at `~/.codemender/command_policy.yaml` . You can uncomment or add rules under two keys:

- **`block`** : A list of binary names to block across all shell pipelines, subshells, and command substitutions (for example, `curl` , `wget` , `ssh` , `sudo` , `rm` ).
- **`block_patterns`** : A list of regular expressions matched against each command segment (for example, `'\bgit\s+(push|commit|rebase|reset\s+--hard|clean)\b'` ).

To bypass `command_policy.yaml` enforcement for a single command invocation, pass the `--allow-all-commands` flag.

- **`output: { plain: false }`**
  - **What it means:** Controls whether the CodeMender CLI replaces emoji, Unicode symbols, and terminal colors with ASCII text across CLI output and formatted reports.
  - **Why this is the default:** Rich terminal styling and status icons make interactive scans and exported reports easier to scan. Set `plain` to `true` for CI/CD logs, screen readers, or minimal terminals. For precedence rules and flag overrides, see [Configure plain text output](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#plain-text-output) .

> **Summary:** Treat `config.yaml` and `command_policy.yaml` as your agent policy documents. In local development, keep the built-in sandbox enabled ( `sandbox.enabled: true` or the `--sandbox` flag) and keep `tools.confirm_commands: true` and `tools.confirm_writes: true` to safeguard your environment. Only disable these protections when running inside isolated, disposable virtual machines or CI/CD pipelines.

## Execution sandboxing

To safeguard your workstation against unintended file modifications or unexpected tool side effects, the CodeMender CLI runs inside an OS-level sandbox by default. You can disable sandboxing persistently in [configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#sandbox-configuration) or bypass it per-command using CLI flags.

Although this sandboxing offers an initial layer of defense on your workstation, it offers weaker security protection than running the agent in a fully isolated virtual machine (VM):

- **Linux** : Uses kernel namespaces ( `CLONE_NEWNS` , `CLONE_NEWUSER` , etc.) and `seccomp` filters to isolate mount points and restrict system calls.
- **macOS** : Uses the built-in `sandbox-exec` (Seatbelt) mechanism.
- **Windows (Experimental)** : Uses `AppContainer` isolation and Access Control Lists (ACLs). Sandboxing on Windows is experimental and may require administrative privileges or be incompatible with some system configurations.

### Sandbox behavior

When the sandbox is active:

1.  **File system isolation** : The agent can only access files within allowed directories. During `cm find` , the workspace and allowed roots are mounted **read-only** , so commands can only write to the per-session artifacts directory. Across all commands (including `cm verify` and `cm fix` ), `.git/hooks` , `.git/config` , `.hg/hgrc` , and `.codemender` are mounted read-only so sandboxed commands can't install Git or Mercurial hooks or modify CodeMender configuration.
2.  **Network isolation** : The sandbox blocks outbound network access by default ( `sandbox.network.profile: "permissive-closed"` ). This prevents the agent (or the build tools it invokes) from making unexpected external connections or transmitting data outside the workspace.
3.  **Credential and secret isolation** : The sandbox excludes common host credential directories ( `~/.ssh` , `~/.gnupg` , `~/.aws` , `~/.config/gcloud` , `~/.config/gh` , `~/.kube` , `~/.docker` , and others) and strips environment variables matching secret patterns ( `*_TOKEN` , `*_SECRET` , `*_KEY` , `*_PASSWORD` , `*_CREDENTIALS` , and similar suffixes) before executing commands.

### Network access during build and validation

Because the sandbox enables network isolation by default ( `sandbox.network.profile` defaults to `permissive-closed` ), the agent **cannot access the internet** during tool execution.

This introduces limitations for projects that require fetching external dependencies during the build or verification steps (for example, running `npm install` , `pip install` , or `go get` as part of the `build.command` ). If your build process attempts to access external web services, it will fail.

#### Handling network dependencies

If your project requires network access for builds or tests, you have the following options:

- **Pre-fetch dependencies** : Install all required dependencies on the host system before running `cm` commands, so the build command does not need network access.

- **Enable network access in the sandbox** : Change the network profile in your `config.yaml` to allow outbound connections:

  ```
  sandbox:
    network:
      profile: "permissive-open"
  ```

  > **Note:** Granular allow-listing of specific domains or URL patterns (such as only allow-listing `npmjs.org` ) is not yet supported; `permissive-open` grants full outbound access to the sandbox.

- **Disable the sandbox for a run** : Run the command with the `--sandbox=false` flag to disable the OS-level sandbox (including network isolation) for that execution.

### Sandbox configuration

You can configure and control the sandbox and security boundaries using the following options:

- **Persistent configuration ( `config.yaml` and `command_policy.yaml` )** : Customize sandbox behavior, file system mounts, network access, and command denylists in `config.yaml` and `command_policy.yaml` . See [Configuration parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#configuration-file) and [Command policy](https://docs.cloud.google.com/gemini-enterprise-agent-platform/agents/codemender/set-up-environment#command-policy) for details.
- **Control the OS-level sandbox ( `--sandbox` )** : Explicitly enable or disable the OS-level sandbox for a single run by passing `--sandbox=true` or `--sandbox=false` to `cm find` , `cm verify` , `cm fix` , or `cm session resume` .
- **Bypass path boundaries ( `--allow-all-paths` )** : Disable the workspace path boundary check for a single run so agent tools can access paths outside the project root and configured `project_paths` (combine with `--sandbox=false` to access host paths that aren't mounted inside the sandbox).
- **Bypass command policy ( `--allow-all-commands` )** : Disable `command_policy.yaml` blocklist enforcement for a single run.

### Choosing an isolation level

Depending on your security requirements and development environment, you can choose the appropriate isolation level for running the CodeMender CLI.

| Method                          | Description                                                                                                                                                                                                         | Advantages                                                                                                                                             | Disadvantages                                                                                                                                                                               |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Built-in sandbox** (OS-level) | Enabled by default; you can disable it in the `config.yaml` file or bypass it using CLI flags. Uses built-in OS features (namespaces/seccomp, `sandbox-exec` , `AppContainer` (Experimental)) to isolate execution. | **Lightweight** ; zero startup overhead; direct access to local workspace tools with fine-grained control. Recommended for everyday local development. | Security relies on OS kernel features; less isolated than a full VM; Windows support is experimental and may require administrative privileges or be incompatible with some configurations. |
| **Containers**                  | Running the agent in a container (for example, Docker).                                                                                                                                                             | Good isolation; standardized environment.                                                                                                              | Requires container runtime; can be heavy; disallows direct interaction with tools on the local machine.                                                                                     |
| **Full VMs**                    | Running the agent in a dedicated VM.                                                                                                                                                                                | Maximum security; complete isolation.                                                                                                                  | High resource overhead; slow startup; disallows direct interaction with tools on the local machine.                                                                                         |

## Configure plain text output

By default, the CodeMender CLI uses emoji, Unicode symbols, and terminal colors in interactive output and formatted reports. To use ASCII-only output in CI/CD logs, screen readers, or minimal terminals, enable plain text mode. The CodeMender CLI checks these settings from highest to lowest precedence:

1.  Pass the `--plain` flag to any `cm` command for a single run, or pass `--plain=false` to override environment and configuration settings:

    ```
    cm --plain find .
    ```

2.  Set the `CM_PLAIN` environment variable to `true` or `1` to enable plain text output across commands, or to `false` or `0` to turn it off:

    ```
    export CM_PLAIN=true
    ```

3.  Set `output.plain` to `true` in your `~/.codemender/config.yaml` file:

    ```
    output:
      plain: true
    ```

4.  Run an interactive session in a terminal where `TERM=dumb` , which enables plain text output automatically.

Plain text mode replaces status emoji with ASCII tags such as `[OK]` , `[INFO]` , `[WARN]` , `[ERROR]` , `[PASS]` , and `[FAIL]` . CodeMender also turns off animated spinners and in-place line rewrites, and renders ASCII table borders. In `cm report` , plain text mode removes UI emoji from `table` , `md` , and `html` formats without changing `json` or `sarif` output or code diffs.

Redirected files and non-interactive CI/CD streams keep `plain` set to `false` by default so that exported Markdown and HTML reports preserve status icons. To remove emoji and Unicode symbols in CI/CD logs, set `CM_PLAIN=true` , pass `--plain` , or set `output.plain: true` . Terminal color escapes are omitted automatically on non-interactive streams and when you set the `NO_COLOR` environment variable.

## Telemetry

To help us monitor and improve product health, we collect anonymous telemetry data through the CLI. We fully anonymize all collected data, which includes basic usage metrics and performance diagnostics. Telemetry never collects or transmits source code, file contents, findings, patches, or user identities.

By default, telemetry is enabled. If you want to disable telemetry, set the `CM_TELEMETRY_OPT_OUT` environment variable to `1` or `true` .

## Updating the CLI

CodeMender has a built-in update mechanism to ensure you are running the latest version of the CLI.

### Automatic update checks

By default, the CodeMender CLI automatically checks for updates in the background when you run commands:

- **Throttling** : To minimize overhead, the automatic check runs at most once every 24 hours.
- **Interactive Terminal (TTY) Required** : The CLI only checks for updates and prompts you when running in an interactive terminal. In non-interactive environments (such as CI/CD pipelines or scripts), the check is skipped and a warning is logged to `stderr` at most once a day.
- **Prompting** : If a new version is available, you'll be prompted on `stderr` : `none 🆕 A new CodeMender release is available: 1.1.0 Update now? (y/N):` If you choose yes ( `y` or `yes` ), CodeMender downloads the update, replaces the binary, and exits. You must run your command again to execute it with the new version. If you choose no, the update is skipped and your original command executes.
- **Offline Tolerance** : If you are offline or the release repository is unreachable, the check fails silently and CodeMender continues to execute your command.
- **Bypassing** : You can bypass the automatic update check by passing the `--yes` or `-y` flag to any command.

### Manual updates ( `cm update` )

You can force CodeMender to check for and apply updates immediately by running the `update` command:

```
cm update
```

The `cm update` command:

- Ignores the 24-hour throttle.
- Downloads and applies the update immediately without prompting (non-interactive).
- Doesn't require an interactive terminal (safe for scripts and configuration management).

If the CLI is installed in a system directory that requires elevated permissions, run the update with `sudo` :

```
sudo cm update
```
