---
name: documents/docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment
uri: https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment
title: Install and configure the CLI
description: Learn how to download the CodeMender CLI, configure Google Cloud credentials, and initialize your workspace.
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

To begin using CodeMender, set up your Google Cloud project, download and install the CLI, configure your credentials, and initialize your workspace.

### Project setup and IAM permissions

Before downloading the CLI and configuring credentials, ensure that the target Google Cloud project is set up correctly with the required APIs and permissions.

#### Required APIs

Ensure the following Google Cloud APIs are enabled in your project:

1.  **Vertex AI API** ( `aiplatform.googleapis.com` ) — Powers the streaming and management of active sessions.
2.  **Cloud Resource Manager API** ( `cloudresourcemanager.googleapis.com` ) — Validates user authentication states and project metadata.

#### Recommended predefined IAM role

To run the CLI commands, users should be assigned the following IAM role:

  - **Vertex AI User** ( `roles/aiplatform.user` ) — Allows users to create, stream, and manage active sessions.

### Download and install CodeMender CLI

The CodeMender CLI binaries are hosted in Artifact Registry. Choose the tab for your operating system to download and install the CLI.

> **Note:** CodeMender is currently available to a limited set of customers in Public Preview. Contact your sales team to get access.

### Linux x86\_64

To download and install CodeMender CLI for Linux (x86\_64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-linux-amd64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-linux-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-amd64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-linux-amd64.zip
        chmod +x cm
        sudo mv cm /usr/local/bin/cm

### Linux ARM64

To download and install CodeMender CLI for Linux (ARM64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-linux-arm64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-linux-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-linux-arm64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-linux-arm64.zip
        chmod +x cm
        sudo mv cm /usr/local/bin/cm

### macOS Intel

To download and install CodeMender CLI for macOS (Intel):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-darwin-amd64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-darwin-amd64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-amd64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-darwin-amd64.zip
        chmod +x cm
        mv cm /usr/local/bin/cm

### macOS Apple silicon

To download and install CodeMender CLI for macOS (Apple silicon):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command:
        
            gcloud artifacts generic download \
              --project=cmoc-prod \
              --location=us \
              --repository=codemender-cli-production \
              --package=cm \
              --version=stable \
              --name=cm-darwin-arm64.zip \
              --destination=./
    
      - **curl:** Run the following command:
        
            curl -L -o cm-darwin-arm64.zip "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-darwin-arm64.zip:download?alt=media"

2.  Install the CLI:
    
        unzip cm-darwin-arm64.zip
        chmod +x cm
        mv cm /usr/local/bin/cm

### Windows x86\_64

To download and install CodeMender CLI for Windows (x86\_64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command in PowerShell:
        
            gcloud artifacts generic download `
              --project=cmoc-prod `
              --location=us `
              --repository=codemender-cli-production `
              --package=cm `
              --version=stable `
              --name=cm-windows-amd64.zip `
              --destination=./
    
      - **PowerShell:** Run the following command:
        
            Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-amd64.zip:download?alt=media" -OutFile cm-windows-amd64.zip

2.  Install the CLI:
    
        Expand-Archive -Path cm-windows-amd64.zip -DestinationPath ./
        # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)

### Windows ARM64

To download and install CodeMender CLI for Windows (ARM64):

1.  Download the package using one of the following methods:
    
      - **gcloud CLI:** Run the following command in PowerShell:
        
            gcloud artifacts generic download `
              --project=cmoc-prod `
              --location=us `
              --repository=codemender-cli-production `
              --package=cm `
              --version=stable `
              --name=cm-windows-arm64.zip `
              --destination=./
    
      - **PowerShell:** Run the following command:
        
            Invoke-WebRequest -Uri "https://artifactregistry.googleapis.com/download/v1/projects/cmoc-prod/locations/us/repositories/codemender-cli-production/files/cm%3Astable%3Acm-windows-arm64.zip:download?alt=media" -OutFile cm-windows-arm64.zip

2.  Install the CLI:
    
        Expand-Archive -Path cm-windows-arm64.zip -DestinationPath ./
        # Move cm.exe to a permanent folder and add it to your system PATH (e.g. Environmental Variables)

### Configure Google Cloud credentials

Because the CodeMender CLI interacts with the cloud-hosted reasoning engine over the Interactions API, you must configure Google Cloud Application Default Credentials (ADC) in your environment.

To authenticate, run the following command and follow the login prompts:

    gcloud auth application-default login

## Initialize the workspace

Once you have authenticated, your next step is to initialize CodeMender in your local environment. Initializing CodeMender prepares your local workspace by creating state-tracking files and establishing connection settings to the cloud-hosted reasoning engine.

Run `cm init` from the root directory of your codebase to create local state tracking files and establish baseline configurations:

    cm init

Use the --verify flag to test connectivity to the cloud-hosted reasoning engine and verify workspace settings:

    cm init --verify

> **Note:** If you encounter the message `Resource setup has just started. Please try again shortly.` , initial resource provisioning is underway and typically completes within a few minutes.

## Configuration parameters ( `config.yaml` )

The primary goal of `config.yaml` is to **align CodeMender's agent behaviors with your local system's security, environment constraints, and performance needs** .

Since the hosted AI agent executes local commands (like building code, running tests, or editing files) using your local daemon client, this configuration file acts as the boundary defining what the agent is and isn't allowed to do.

### Usage

  - **Location:** By default, the CLI looks for this file in your initialized workspace (usually `.codemender/config.yaml` or a global configuration directory like `~/.config/codemender/config.yaml` ).
  - **Execution:** When you run commands such as `cm find` , `cm verify` , or `cm fix` , the local client reads this file to set up safety parameters, apply system bypasses, and specify which files or directories to ignore.

### Core default settings

Here is what the core default parameters mean:

  - **`human_confirmation: true` (or `require_confirmation: true` )**
    
      - **What it means:** By default, CodeMender **cannot** modify any file on your disk or execute shell commands without explicitly prompting you for a `[Y/n]` confirmation in the terminal.
      - **Why it's default:** CodeMender may generate speculative patches or attempt to run exploit scripts to verify a vulnerability. Forcing human confirmation helps prevent accidental system changes or unauthorized code execution in your local environment.
      - **Bypass:** For non-interactive CI/CD pipelines, this can be set to `false` .

  - **`confirm_writes: false`**
    
      - **What it means:** Disables interactive prompts for file modifications, allowing the CodeMender agent to write security patches and modify source files directly to your local disk without waiting for human approval.
      - **Why it's default:** By default, this safety guardrail is set to `true` to enforce a "Human-in-the-Loop" workflow. Because CodeMender acts on your local codebase, requiring manual confirmation (for example, `Write? [Y/n]` ) prevents the agent from making speculative, incorrect, or destructive modifications to your source files. You should only switch this to `false` when running in isolated, disposable sandboxes or automated, headless CI/CD pipelines.

  - **`include: [".py", ".java", ".go", ".js", ".ts", ".c", ".cc", ".cpp", ".h", ".rb", ".php"]`**
    
      - **What it means:** Defines the explicit list of file extensions that CodeMender is authorized to ingest and analyze when scanning your workspace. Any file in your repository with an extension not specified in this list is automatically skipped.
      - **Why it's default:** By default, this list is restricted to major programming languages to maximize scanning efficiency and prevent the agent from wasting time and tokens on irrelevant text files, build artifacts, or binary files. However, because modern applications often embed vulnerabilities in deployment configs or automation tools, it is highly recommended to manually expand this default list to include configuration files, script formats, and IaC files (for example, `.sh` , `.xml` , `.yaml` , `.properties` , `.json` ) so CodeMender doesn't silently ignore them.

  - **`exclude_paths: ["node_modules", "vendor", "dist", "bin"]`**
    
      - **What it means:** CodeMender will completely skip these directories during workspace scanning and code analysis.
      - **Why it's default:** Large dependency or build folders trigger a massive latency and token penalty. Keeping these excluded by default ensures high performance and rapid response times.

  - **`project_paths: []`**
    
      - **What it means:** A list of directory paths that CodeMender is allowed to access (read/write) during tool execution.
      - **Why it's default:** By default, it is empty, which restricts the agent to the scan target directory, the `.codemender` workspace directory, and `/tmp` . If your build or test process requires accessing files outside these directories, you must add those paths here.

  - **`sandbox`** :
    
      - **What it means:** Configuration block for the process-level sandbox environment.
      - **Sub-parameters:**
          - **`enabled: false`** : (Boolean) Enables or disables the sandbox. When set to `true` , the agent runs tools inside the local sandbox. When set to `false` (default), the agent runs tools directly on the host system without isolation.
          - **`mounts`** : (Object)
              - **`target_dir: "."`** : (String) The directory to mount as the active workspace inside the sandbox. Relative paths are resolved against the workspace root.
          - **`network`** : (Object)
              - **`profile: "permissive-closed"`** : (String) Outbound network access profile inside the sandbox. Granular allow-listing of specific domains or URL patterns is not yet supported. Supported profiles:
                  - `permissive-closed` (Default): Complete network isolation; all outbound connections are blocked.
                  - `permissive-open` : Allows full outbound network access.

  - **`security`** :
    
      - **What it means:** Configuration block for security policies.
      - **Sub-parameters:**
          - **`protected_files: []`** : (List of Strings) Files or directories on the host system that should be mounted **read-only** inside the sandbox to protect them from modification (e.g., `["~/.ssh/*"]` ). Supports path expansion ( `~` ) and wildcards ( `*` ).

  - **`model: "gemini-3.5-flash"`**
    
      - **What it means:** The default intelligence engine powering the backend reasoning loops.
      - **Why it's default:** `gemini-3.5-flash` offers the optimal balance of speed, cost, and analytical reasoning required to suggest patches. (Users can override this to `gemini-3.1-pro` for deeper, more complex reasoning when needed).

  - **`vcs: { type: "git" }`**
    
      - **What it means:** Defines the type of version control system used by your project through the `vcs` key. If left unconfigured, the tool attempts to automatically identify Git or Mercurial repositories. If `vcs` is set to `none` by default, the CLI outputs a warning but continues execution without VCS functionality. CodeMender relies on this setting to manage speculative security fixes, track codebase modifications, and integrate with your local repository.
      - **Why it's default:** CodeMender supports Git, Mercurial, or custom VCS configurations. Git is the default as it is the industry standard for version control tracking, ensuring seamless diff integration and rollback safety.

  - **`build: { command: "make build && make test" }`**
    
      - **What it means:** Defines the exact shell command that CodeMender executes to compile and build your project, as well as run your unit and regression tests.
      - **Why it's default:** Setting a build and test command is critical for the verification workflow. It allows CodeMender to compile your project and run your existing test suite in the isolated sandbox environment to prove that the generated security patch successfully mitigates the vulnerability without breaking existing application logic.

> **Summary recommendation:** Treat `config.yaml` as your agent policy document. In local development, we highly recommend that you enable the built-in sandbox ( `sandbox.enabled: true` or the `--sandbox` flag) and keep `human_confirmation: true` to safeguard your environment. Only disable these protections when running inside isolated, disposable sandbox virtual machines or CI/CD pipelines.

## Execution sandboxing

To safeguard your workstation against unintended file modifications or unexpected tool side effects, you can run the CodeMender CLI inside an OS-level sandbox. Sandboxing is disabled by default, but can be enabled persistently in [configuration](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#sandbox-configuration) or per-command using CLI flags.

While this sandboxing offers an initial layer of defense on your workstation, it offers weaker security protection than running the agent in a fully isolated virtual machine (VM):

  - **Linux** : Uses kernel namespaces ( `CLONE_NEWNS` , `CLONE_NEWUSER` , etc.) and `seccomp` filters to isolate mount points and restrict system calls.
  - **macOS** : Uses the built-in `sandbox-exec` (Seatbelt) mechanism.
  - **Windows (Experimental)** : Uses `AppContainer` isolation and Access Control Lists (ACLs). Sandboxing on Windows is experimental and may require administrative privileges or be incompatible with some system configurations.

### Sandbox behavior

When the sandbox is active:

1.  **File system Isolation** : The agent can only read and write files within allowed directories. Any writes outside these directories are redirected to a temporary in-memory file system (tmpfs) and don't affect your host system.
2.  **Network Isolation** : Outbound network access from within the sandbox is blocked by default. This prevents the agent (or the build tools it invokes) from making unexpected external connections or transmitting data outside the workspace.

### Network access during build and validation

Because network isolation is enabled by default in the sandbox ( `sandbox.network.profile` defaults to `permissive-closed` ), the agent **cannot access the internet** during tool execution.

This introduces limitations for projects that require fetching external dependencies during the build or verification steps (for example, running `npm install` , `pip install` , or `go get` as part of the `build.command` ). If your build process attempts to access external web services, it will fail.

#### Handling network dependencies

If your project requires network access for builds or tests, you have the following options:

  - **Pre-fetch dependencies** : Ensure all required dependencies are already installed on the host system before running `cm` commands, so the build command does not need network access.

  - **Enable network access in the sandbox** : Change the network profile in your `config.yaml` to allow outbound connections:
    
        sandbox:
          network:
            profile: "permissive-open"
    
    > **Note:** Granular allow-listing of specific domains or URL patterns (such as only allow-listing `npmjs.org` ) is not yet supported; `permissive-open` grants full outbound access to the sandbox.

  - **Bypass the sandbox** : Run the command with the `--unrestricted` flag to disable the sandbox and file system boundaries entirely for that execution.

### Sandbox configuration

You can configure and control the sandbox using the following options:

  - **Persistent Configuration ( `config.yaml` )** : You can enable and customize sandbox behavior, file system mounts, network access, and security policies by adding `sandbox` , `execution` , and `security` blocks to your `config.yaml` file. See [Configuration parameters](https://docs.cloud.google.com/gemini-enterprise-agent-platform/codemender/set-up-environment#configuration-file) for details.
  - **Enabling the sandbox using the CLI ( `--sandbox` )** : You can temporarily enable the sandbox for a single run by passing the `--sandbox` flag to `cm find` , `cm verify` , or `cm fix` .
  - **Bypassing isolation using the CLI ( `--unrestricted` )** : If the sandbox is enabled, you can temporarily bypass all sandbox protections for a single run by passing the `--unrestricted` flag. This disables the file system path boundaries (allowing the agent to access any path on your host) and disables the OS-level container isolation entirely (including network isolation).

### Choosing an isolation level

Depending on your security requirements and development environment, you can choose the appropriate isolation level for running the CodeMender CLI.

| Method                          | Description                                                                                                                                                                         | Advantages                                                                                                                                             | Disadvantages                                                                                                                                                                               |
| :------------------------------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Built-in sandbox** (OS-level) | Disabled by default; can be enabled using config or CLI flags. Uses built-in OS features (namespaces/seccomp, `sandbox-exec` , `AppContainer` (Experimental)) to isolate execution. | **Lightweight** ; zero startup overhead; direct access to local workspace tools with fine-grained control. Recommended for everyday local development. | Security relies on OS kernel features; less isolated than a full VM; Windows support is experimental and may require administrative privileges or be incompatible with some configurations. |
| **Containers**                  | Running the agent in a container (e.g., Docker).                                                                                                                                    | Good isolation; standardized environment.                                                                                                              | Requires container runtime; can be heavy; disallows direct interaction with tools on the local machine.                                                                                     |
| **Full VMs**                    | Running the agent in a dedicated VM.                                                                                                                                                | Maximum security; complete isolation.                                                                                                                  | High resource overhead; slow startup; disallows direct interaction with tools on the local machine.                                                                                         |

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

    cm update

The `cm update` command:

  - Ignores the 24-hour throttle.
  - Downloads and applies the update immediately without prompting (non-interactive).
  - Doesn't require an interactive terminal (safe for scripts and configuration management).

If the CLI is installed in a system directory that requires elevated permissions, run the update with `sudo` :

    sudo cm update
